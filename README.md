# Annual Spending Dashboard

A single-file, dependency-free web dashboard for tracking annual spending. Enter your fortnightly (or weekly/monthly/annual) take-home pay, add expenses as you think of them, and see your annualised totals, per-fortnight costs, category breakdown, and surplus/savings rate — all in the browser, with no server, no account, and no data leaving your devices (except the optional cloud sync you configure yourself).

## Features

- **Income input** with weekly / fortnightly / monthly / annual pay frequencies, normalised to annual and fortnightly equivalents (26 fortnights per year)
- **Expense entry** with flexible frequencies — weekly, fortnightly, monthly, quarterly, annual, or one-off costs (rego, holidays, gifts)
- **Summary cards** — fortnightly income and spending, left per fortnight, annual totals, annual surplus, and savings rate
- **Category breakdown** — annualised bars per category with per-year, per-fortnight, and percent-of-income figures
- **Expense management** — inline edit/delete, search, category filter, and sorting (including by annual cost)
- **Automatic persistence** — every change saves instantly to browser localStorage
- **Optional linked save file** (Chrome/Edge desktop) — auto-writes a live JSON backup to a location you choose via the File System Access API, surviving cleared browser data
- **Optional cross-device sync** — sync the same inputs across your computer and phone using a secret GitHub Gist as private storage (see below)
- **Export** to CSV (opens directly in Excel, with totals) and JSON, plus JSON import for restores or moving between machines
- **Responsive** — works on desktop and phone, including an Add to Home Screen mode on iOS

## Usage

### Option A: just open the file

Download `spending-dashboard.html` and open it in any modern browser. Data is stored in that browser's localStorage and persists between sessions.

> **Note:** if you open the file from a mobile Files app, storage may not persist between openings. Use Option B on phones.

### Option B: host it with GitHub Pages (recommended)

1. In your repository: **Settings → Pages**
2. Under **Build and deployment**, set Source to **Deploy from a branch**, choose `main` and `/ (root)`, then Save
3. After a minute or two, the dashboard is live at `https://<username>.github.io/<repo>/spending-dashboard.html`

Hosting gives the page a stable origin, which makes localStorage reliable across sessions on every device — including iPhone (open in Safari, then Share → Add to Home Screen for an app-like experience).

## Cloud sync across devices (optional)

To see the same income and expenses on every device, the dashboard can store its data in a **secret GitHub Gist** — a private JSON file only you can access. No server of your own is needed; the GitHub API allows the page to read and write the Gist directly from the browser.

Setup:

1. Create a classic token at [github.com/settings/tokens/new?scopes=gist](https://github.com/settings/tokens/new?scopes=gist&description=Spending%20dashboard%20sync) with **only the `gist` scope** enabled. (Fine-grained tokens don't support Gists.)
2. Open the dashboard on your first device, scroll to **Cloud sync across devices**, paste the token, and click **Connect** — a secret Gist is created automatically and its ID is remembered.
3. On each other device, open the dashboard, paste the same token, and enter the Gist ID shown after the first connect (or find it in your [Gists list](https://gist.github.com)).

Once connected, the dashboard pulls the latest data when the page opens or comes back to the foreground, and pushes changes about two seconds after you make them. Conflicts are resolved last-writer-wins, so avoid editing on two devices at the same time. The token is stored in each browser's localStorage and never sent anywhere except GitHub's API.

## How your data is stored

| Layer | Where | Notes |
|---|---|---|
| localStorage | This browser, this device | Always on. Survives restarts. Lost if browser data is cleared. |
| Linked JSON file | A file path you choose | Optional, desktop Chrome/Edge only. Written on every change (debounced). Survives cleared browser data. |
| Secret GitHub Gist | Your GitHub account | Optional. Cross-device sync. Pull on open, push on change. |
| Manual exports | Wherever you save them | CSV for Excel; JSON for backups. |

## Browser support

| Browser | Status |
|---|---|
| Chrome / Edge / Brave (desktop) | Fully supported, including linked save file |
| Firefox, Safari (desktop) | Fully supported; linked save file unavailable (uses cloud sync / exports instead) |
| iOS Safari / Android Chrome | Fully supported; host the file (Option B) for reliable persistence |

## Files

- `spending-dashboard.html` — the entire application (HTML, CSS, and JavaScript in one file)

## License

MIT
