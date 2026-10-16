# $200 → $5K Dashboard — GitHub Deployment Troubleshooting

**Date:** 2026-10-15 19:41 CDT  
**Repository:** `sayntchase-rgb/parent-daily-display`  
**Dashboard path:** `fivek-dashboard/`  
**Branch:** `main`

## Status Dashboard

| Check | Status | Evidence / Meaning |
|---|---|---|
| Repository exists | PASS | `sayntchase-rgb/parent-daily-display` is public and accessible |
| Dashboard folder exists on `main` | PASS | `fivek-dashboard/` is present at repository root |
| `index.html` exists | PASS | Dashboard source is committed |
| PWA manifest exists | PASS | `manifest.webmanifest` is committed |
| Service worker exists | PASS | `service-worker.js` is committed |
| App icon exists | PASS | `icon.svg` is committed |
| GitHub Pages workflow exists | PASS | `.github/workflows/deploy-fivek-dashboard.yml` is committed |
| Workflow triggers | PASS | GitHub Actions has run the workflow |
| Checkout step | PASS | Repository checkout completed successfully |
| Configure Pages step | **FAIL** | Pages site is not enabled/configured for this repository |
| Upload Pages artifact | BLOCKED | Skipped because Configure Pages failed |
| Deploy Pages site | BLOCKED | Skipped because Configure Pages failed |
| Public dashboard URL | NOT LIVE | No Pages deployment has completed yet |
| Android home-screen install | BLOCKED | Requires the HTTPS Pages site to be live first |

## Issue 1 — Why the dashboard was hard to find

The dashboard was **not created as a new standalone repository**. It was added inside the existing repository:

`parent-daily-display/fivek-dashboard/`

Therefore it will not appear as a separate repository named `FiveK-Dashboard` in the GitHub repository list.

### Direct repository location

`https://github.com/sayntchase-rgb/parent-daily-display/tree/main/fivek-dashboard`

## Issue 2 — GitHub Pages deployment failure

### Failed workflow

Workflow:

`Deploy $5K Dashboard to GitHub Pages`

Latest failed run ID:

`38830187840`

Job:

`deploy`

Job ID:

`116746945356`

### Exact failing step

`Setup Pages` using:

`actions/configure-pages@v5`

### Exact GitHub Actions error

> Get Pages site failed. Please verify that the repository has Pages enabled and configured to build using GitHub Actions. Error: Not Found.

### Interpretation

The workflow file itself is being recognized and executed. Repository checkout succeeds. The failure happens because GitHub does not yet have a Pages site configured for this repository.

This is **not** a missing dashboard-file problem and **not** a checkout problem.

## Root Cause

**GitHub Pages has not been enabled/configured with GitHub Actions as the publishing source for `parent-daily-display`.**

The workflow has the normal Pages permissions:

- `contents: read`
- `pages: write`
- `id-token: write`

However, `actions/configure-pages@v5` cannot find an enabled Pages site, so deployment stops before artifact upload.

## Corrective Action — One-Time GitHub Setting

Open:

`https://github.com/sayntchase-rgb/parent-daily-display/settings/pages`

Then set:

**Settings → Pages → Build and deployment → Source → GitHub Actions**

After saving that setting, open:

`https://github.com/sayntchase-rgb/parent-daily-display/actions/workflows/deploy-fivek-dashboard.yml`

Then run:

**Run workflow → main → Run workflow**

Alternatively, any later commit touching `fivek-dashboard/**` or the deployment workflow will trigger it automatically.

## Expected Successful Pipeline

```text
Checkout
   ↓
Setup Pages
   ↓
Upload dashboard artifact
   ↓
Deploy to GitHub Pages
   ↓
HTTPS dashboard URL
   ↓
Install on Android home screen
```

## Expected Site URL

After a successful Pages deployment, the workflow should expose the actual deployment URL. For this repository, the expected base URL is typically:

`https://sayntchase-rgb.github.io/parent-daily-display/`

Do not treat that URL as confirmed live until the deployment job reports success.

## Phone Shortcut / PWA

After the HTTPS Pages site is live:

1. Open the dashboard URL in Chrome on Android.
2. Use the in-dashboard **Install $5K Dashboard on this phone** control if Chrome exposes the install prompt.
3. Otherwise use Chrome **⋮ → Install app** or **Add to Home screen**.
4. Confirm installation.

The dashboard stores tracking data in browser/local app storage on that device.

## Important Technical Note

The `enablement` input on `actions/configure-pages@v5` can attempt to enable Pages, but GitHub's current action documentation says that automatic enablement requires a token other than the normal workflow `GITHUB_TOKEN` with additional Pages/administration permissions. Therefore, changing the repository Pages source manually is the cleaner one-time fix for the current setup.

## Current Troubleshooting State

**ROOT CAUSE IDENTIFIED — FIX PENDING ONE ACCOUNT-SIDE GITHUB PAGES SETTING.**

Once Pages is enabled with **GitHub Actions** as the source, rerun the deployment workflow and verify all five stages complete successfully.
