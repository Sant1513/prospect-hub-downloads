# Prospect Hub: team downloads

## 👉 [Install guide (start here)](https://sant1513.github.io/prospect-hub-downloads/)

**Latest version: v0.3.2**. [Download the setup zip](https://github.com/Sant1513/prospect-hub-downloads/releases/latest/download/prospect-hub-setup.zip): on Windows run setup.cmd; on Mac/Linux run bash setup.sh.

This repository holds only the built files; the source code is private.

---

# Prospect Hub: install and update (team members)

**Install guide with copy buttons: https://sant1513.github.io/prospect-hub-downloads/**. No GitHub account is needed.

You need **Google Chrome**, plus **Node.js 24 or newer** (from https://nodejs.org, the "LTS" installer). Check with `node -v` in a terminal.

## 1. Install the helper

The helper keeps your data on this computer and syncs it to the team.

### Windows (recommended: paste one command)

This works even when **Smart App Control** blocks downloaded files. Open **PowerShell** (Start → type `PowerShell` → Enter), paste everything below, and press **Enter**:

```powershell
$ErrorActionPreference = 'Stop'
if (-not (Get-Command node -ErrorAction SilentlyContinue)) { Start-Process 'https://nodejs.org/en/download'; throw 'Install Node.js (LTS), then paste this again.' }
if ([int](node -p "process.versions.node.split('.')[0]") -lt 24) { Start-Process 'https://nodejs.org/en/download'; throw 'Node.js 24 or newer is needed. Install it, then paste this again.' }
$zip = "$env:TEMP\prospect-hub-setup.zip"; $tmp = "$env:TEMP\prospect-hub-setup"; $app = "$env:LOCALAPPDATA\ProspectHub"
Invoke-WebRequest 'https://github.com/Sant1513/prospect-hub-downloads/releases/latest/download/prospect-hub-setup.zip' -OutFile $zip -UseBasicParsing
Expand-Archive $zip $tmp -Force
Get-ChildItem $tmp -Recurse | Unblock-File
if (Test-Path "$app\helper-app\install-service.mjs") { node "$app\helper-app\install-service.mjs" --remove }
New-Item -ItemType Directory -Force "$app\helper-app", "$app\extension" | Out-Null
Copy-Item "$tmp\Prospect Hub setup\helper\*" "$app\helper-app" -Recurse -Force
Copy-Item "$tmp\Prospect Hub setup\extension\*" "$app\extension" -Recurse -Force
node "$app\helper-app\install-service.mjs"
Start-Sleep 3; Start-Process 'http://127.0.0.1:47615/'; explorer "$app\extension"
Write-Host "Done. In Chrome: chrome://extensions > Developer mode ON > Load unpacked > $app\extension" -ForegroundColor Green
```

It installs the helper so it starts at every sign-in, then opens the helper page (which shows your **pairing code**) and the extension folder.

**If the helper page doesn't open:** Smart App Control may have blocked the start-at-sign-in entry. Start the helper by hand and keep that PowerShell window open while you use the extension:

```powershell
node "$env:LOCALAPPDATA\ProspectHub\helper-app\helper.mjs"
```

**Alternative (only when Smart App Control is off):** download `prospect-hub-setup.zip`, extract it, and double-click `setup.cmd`.

### Mac / Linux

Download `prospect-hub-setup.zip` from the install guide, unzip it, open a terminal in that folder, and run `bash setup.sh`.

## 2. Add the extension to Chrome

1. Open `chrome://extensions` (paste it into the address bar).
2. Turn on **Developer mode** (top right).
3. Click **Load unpacked** and choose `%LOCALAPPDATA%\ProspectHub\extension` (Windows) or `~/Library/Application Support/ProspectHub/extension` (Mac).
4. Pin **Prospect Hub** (puzzle-piece icon) and click it to open the side panel.

## 3. Connect to the team

1. In the side panel, enter the pairing code from http://127.0.0.1:47615/.
2. Get a one-time **enrollment code** from the owner (Dashboard → Sync → Add a helper device).
3. Side panel → **Settings → Enroll**. Master URL: `https://abhishesh.tail66d6e3.ts.net:8443`. Enter the code.

## Daily use

1. On LinkedIn or **Sales Navigator**, run a **people search** with any filters. On Sales Navigator, scroll to the bottom of the results once so all 25 leads load.
2. Side panel → **Collect → LinkedIn page → Capture people on this page**.
3. Check the list: new people are pre-selected, and people the team already saved are marked. Click **Save**.
4. Go to the next results page on LinkedIn and capture again.

Leads captured from Sales Navigator are saved with their **Sales Navigator lead link** (`https://www.linkedin.com/sales/lead/…/`), which opens for anyone with a Sales Navigator seat. Sales Navigator pages don't show the public `/in/name/` link. **To get a lead's public link:** open the lead in Sales Navigator, then in the side panel click **Get public link**. If Sales Navigator hides it, follow the panel's instructions: click "View LinkedIn profile", and on the profile page click **Use this page**. Exports then show the public link in "LinkedIn Profile URL" and keep the Sales Navigator link in its own column. The same person captured from both searches is stored as two records.

**Fill in many public links quickly (needs a Sales Navigator seat):** on a LinkedIn tab, open **Collect → LinkedIn page**. The blue box shows how many Sales Navigator leads are missing a public link, team-wide. Each click of **Next lead** opens one lead in that tab, reads its "View LinkedIn profile" link and saves it for everyone, so it shows up in the sheet and in exports. If a lead has no link, it is skipped on this computer (you can try skipped leads again later). Nothing opens on its own: every lead is one click.

Everything is saved on your computer right away. It syncs to the team database whenever the master is reachable, even if you were offline, and the team Google Sheet updates within a minute after that. The bar at the top of **Collect** shows how many changes are still waiting on your laptop. Click **Sync now** to send them immediately. If it says it **can't reach the master**, check your internet connection and ask the owner whether the master PC is on and awake. Nothing is lost; it sends as soon as the master is back. Sync never creates duplicate rows in the sheet: each person has one row, matched by Record ID. The bar also has an **Open team sheet** link.

**Download a CSV of the team's prospects:** side panel → **Export**. Pick dates (Today, Yesterday, Last 7 days, or your own range), **Sourced by** (a teammate and laptop, or everyone), the source (LinkedIn or Sales Navigator), connection degree, a word to search for, or only Sales Navigator leads still missing a public link. Then click **Download CSV**. It has the same columns as the sheet, with each person once. This needs the master to be reachable. The **Saved** tab's *Export CSV* still works offline and exports this laptop's copy.

> LinkedIn's terms restrict tools that copy data from its pages, and LinkedIn can limit accounts that use them. Capture reads only what is on your screen, and only when you click. It never scrolls, pages or opens profiles for you.

## Updating

When the side panel shows **Update available**:

1. **Windows:** paste the same PowerShell command again. **Mac/Linux:** download the new zip and run `bash setup.sh` again. Your data is kept.
2. In `chrome://extensions`, click the **reload** icon on Prospect Hub.

## Uninstall

- **Extension:** remove it in `chrome://extensions`.
- **Helper (Windows):** run `node "$env:LOCALAPPDATA\ProspectHub\helper-app\install-service.mjs" --remove` in PowerShell, then delete `%LOCALAPPDATA%\ProspectHub`. That folder also holds your local data (`helper`), so delete it only after the Sync tab shows nothing pending.
