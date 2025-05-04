# GitHub Actions Cache Cleanup

A GitHub Action to automatically delete unused GitHub Actions caches.

## What it does

- Deletes caches from closed Pull Requests
- Deletes caches from the main branch that haven't been used for X days (default: 7)

## How to use

Create a workflow file in your repository (e.g. `.github/workflows/cleanup-cache.yml`):

```yaml
name: Expire caches
on:
  schedule:
    # Run every Monday at 00:00
    - cron: '0 0 * * 1'
  workflow_dispatch:
    # Allows for manual workflow runs
permissions:
  actions: write
  pull-requests: read
jobs:
  cleanup:
    runs-on: ubuntu-latest
    
    steps:
      - name: Delete unused caches
        uses: [your-username]/cache-cleanup-action@v1
        with:
          # Optional: Change number of days before main branch caches are deleted (default: 7)
          main-branch-retention-days: '14'
