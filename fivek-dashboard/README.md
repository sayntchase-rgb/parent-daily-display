# $200 → $5K Houston Dashboard

Deployed source: `fivek-dashboard/`

## Purpose
Mobile operating dashboard for the 7-day $5K revenue challenge.

## Features
- Leads, conversations, quotes, jobs, revenue, expenses, profit, conversion, ROI
- $5,000 progress tracking
- Houston lead-hunt launchers
- Local browser persistence
- CSV export
- PWA manifest + service worker + install icon

## GitHub Pages
Deployment workflow: `.github/workflows/deploy-fivek-dashboard.yml`

The repository must have **Settings → Pages → Build and deployment → Source: GitHub Actions** enabled before the workflow can publish.

Expected Pages URL after successful deployment:

`https://sayntchase-rgb.github.io/parent-daily-display/`

## Android shortcut
After the site is published, open the Pages URL in Chrome and use **Install app** / **Add to Home screen**. The dashboard also exposes an install button when Chrome makes the PWA install prompt available.
