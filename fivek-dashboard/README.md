# $200 → $5K in 7 Days Dashboard

Deployed source: `fivek-dashboard/`

## Purpose

Mobile revenue command center for the 7-day $5K sprint. The dashboard is a control surface, not the goal. Its job is to convert the project doctrine into measurable operating decisions.

## Project-to-Dashboard Synchronization

The dashboard now mirrors the project's core systems:

- Deep Research
- Market Psychology / Buyer Behavior
- Marketing Strategy & Tactics
- Financial Literacy
- Asset Acquisition & Maintenance
- Compounding
- Scaling
- Documentation
- Troubleshooting

The full project instructions remain the canonical doctrine. The dashboard carries only the fields and rules that change execution.

## Revenue Controls

Tracks:

- $5,000 progress
- cash collected
- expenses
- net profit
- jobs
- average ticket
- ROI
- CAC
- revenue per hour
- remaining revenue gap
- scaling stage
- channel leads, conversations, quotes and conversions

## Decision Cockpit

Operational fields capture:

- current market signal / evidence
- buyer trigger / psychology
- marketing experiment
- current bottleneck
- highest-value next action
- scaling stage
- total hours invested

## Financial Controls

Includes:

- booked-but-uncollected revenue
- tax reserve
- available cash / reserve
- channel economics
- CAC
- ROI
- revenue per labor hour

Rule: unpaid invoices are not cash.

## Asset Acquisition & Maintenance

Captures:

- asset under consideration
- economic purpose
- acquisition / total-cost estimate
- expected benefit
- condition / maintenance status
- next maintenance or recovery action

Acquisition filter: an asset should remove a bottleneck, create revenue, reduce cost, increase capacity, reduce risk, or improve future earning capability.

## Compounding & Scaling

Canonical compounding rule:

> Every useful cycle should increase the productive capacity of the next cycle.

Scaling sequence:

`Validate → Measure → Standardize → Automate → Delegate → Expand`

Scale only validated processes with sound unit economics and reliable fulfillment.

## Document + Troubleshoot

The dashboard contains two persistent logs:

### Running Session Log

`Timestamp → Objective → Actions → Outputs → Decisions → Money Spent → Cash Collected → Lesson → Next Action`

### Troubleshooting Log

`Symptom → Context → Likely Cause → Test → Result → Fix → Verification → Prevention`

## Persistence

Dashboard entries are stored in browser `localStorage` using the existing key:

`houston_200_to_5000_dashboard_v2`

This was intentionally preserved so existing tracking data remains compatible with the upgraded interface.

## Export

The CSV export preserves channel-performance data for external analysis.

## PWA / Cache Troubleshooting

The service worker cache was upgraded to `fivek-dashboard-v4` and now:

- calls `skipWaiting()` during install
- deletes prior dashboard caches during activation
- uses network-first fetching with cache fallback

This reduces the risk of an installed PWA continuing to show the old dashboard after repository updates.

If the phone still shows an old version:

1. close the installed dashboard completely
2. reopen it while online
3. refresh once
4. if still stale, remove the installed PWA/site data and reopen the live Pages site

## GitHub Pages

Deployment workflow: `.github/workflows/deploy-fivek-dashboard.yml`

The repository must have:

**Settings → Pages → Build and deployment → Source: GitHub Actions**

enabled before the workflow can publish.

Expected Pages URL after successful deployment:

`https://sayntchase-rgb.github.io/parent-daily-display/`

Treat the URL as unconfirmed until a deployment run succeeds.

## Governing Rules

1. Revenue is the objective; the dashboard is support infrastructure.
2. Prefer the action with the shortest credible path to revenue.
3. Research must end in a decision or test.
4. Do not scale unvalidated offers or negative unit economics.
5. Protect the $200 starting capital.
6. Turn each successful cycle into reusable productive capacity.
7. Document failures so they are not troubleshot from zero again.
