# $5,000 in 7 Days — Dashboard Synchronization & Troubleshooting Log

## Objective

Synchronize the project's governing systems with the operational $5,000 in 7 Days dashboard and preserve the work as both documentation and troubleshooting knowledge.

## Project Systems Required on the Dashboard

- Deep Research
- Market Psychology / Buyer Behavior
- Marketing Strategy & Tactics
- Financial Literacy
- Asset Acquisition & Maintenance
- Compounding
- Scaling
- Documentation
- Troubleshooting

## Previous State

The dashboard already tracked leads, conversations, quotes, jobs, revenue, expenses, profit, conversion, ROI, average ticket, progress, notes, CSV export, and browser-local persistence.

### Gap

It did not yet expose decision controls for market evidence, buyer psychology, marketing experiments, CAC, revenue per labor hour, booked vs collected cash, asset acquisition / maintenance, current bottleneck, reusable assets / compounding, scaling stage, structured documentation, or structured troubleshooting.

## Changes Executed

### Dashboard

Updated `fivek-dashboard/index.html` with:

- Project Operating System summary
- market signal / evidence
- buyer trigger / psychology
- marketing experiment
- current bottleneck
- highest-value next action
- scaling stage
- hours invested
- CAC
- revenue per hour
- remaining revenue gap
- booked-but-uncollected revenue
- tax reserve
- cash reserve
- asset acquisition economics
- asset condition / maintenance status
- reusable asset capture
- process learning capture
- running session log
- structured troubleshooting log

The existing local-storage key `houston_200_to_5000_dashboard_v2` was preserved to reduce migration risk for existing channel data.

### PWA / Cache

Updated `fivek-dashboard/service-worker.js` from cache `fivek-dashboard-v3` to `fivek-dashboard-v4`.

The worker now:

- calls `skipWaiting()`
- deletes old cache versions
- uses network-first fetch with cache fallback
- claims clients during activation

## Troubleshooting

### Problem 1 — Project / Dashboard Drift

**Symptom:** Project instructions expanded while the dashboard remained the earlier revenue tracker.

**Cause:** Doctrine and implementation were being updated independently.

**Fix:** Established a dashboard synchronization contract and implemented decision-relevant project systems in the dashboard.

**Prevention:** When `/document` or `/troubleshoot` changes decision-relevant project state, audit whether the dashboard requires a matching control, metric, signal, status, or next action.

### Problem 2 — Stale Installed PWA

**Symptom:** An installed phone dashboard may display an older interface after GitHub updates.

**Cause:** The previous service worker used cache-first behavior and did not remove old cache versions.

**Fix:** Bumped the cache and switched to network-first behavior with old-cache cleanup.

**Verification:**

1. complete a successful Pages deployment
2. open the live dashboard while online
3. verify the `Project Operating System` and `Decision Cockpit` sections
4. close and reopen the installed PWA
5. confirm the new version remains visible

### Problem 3 — GitHub Pages Deployment

Historical failure: `actions/configure-pages@v5` could not find a configured Pages site.

Historical root cause: GitHub Pages was not configured to use GitHub Actions as the publishing source.

Required setting:

**Settings → Pages → Build and deployment → Source → GitHub Actions**

This is separate from dashboard application code.

## Governing Rule

> The canonical project document is the doctrine. The dashboard is the execution surface.

Synchronize only information that materially affects revenue, market, conversion, cash, assets, fulfillment, compounding, scaling, reliability, troubleshooting, or next-action decisions.
