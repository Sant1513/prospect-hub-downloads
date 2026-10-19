# Prospect Hub: team downloads

**Latest version: v0.2.1**. Download it from [Releases → latest](https://github.com/Sant1513/prospect-hub-downloads/releases/latest).

This repository holds only the built files; the source code is private.

---

# Prospect Hub: install and update (team members)

Downloads: **https://github.com/Sant1513/prospect-hub-downloads/releases/latest**. No GitHub account is needed.

You need **Google Chrome**, plus **Node.js 24 or newer** for the helper (from https://nodejs.org, the "LTS" or "Current" installer).

## First install (about 5 minutes)

1. **Download** `prospect-hub-helper-<version>.zip` and `prospect-hub-extension-<version>.zip` from the link above.
2. **Helper (keeps your data on this computer and syncs it to the team):**
   1. Unzip the helper into a folder you'll keep, e.g. `Documents\ProspectHub\helper`.
   2. In that folder, open a terminal and run:
      ```
      node install-service.mjs
      ```
      It starts now and every time you sign in to the computer. Check it by opening http://127.0.0.1:47615/ in Chrome; the page shows a **pairing code**.
3. **Extension:**
   1. Unzip the extension into a folder you'll keep, e.g. `Documents\ProspectHub\extension`.
   2. In Chrome, open `chrome://extensions`, turn on **Developer mode** (top right), click **Load unpacked**, and select that folder.
   3. Pin **Prospect Hub** (puzzle-piece icon) and click it to open the side panel.
4. **Connect:**
   1. In the side panel, enter the pairing code from http://127.0.0.1:47615/.
   2. Get a one-time **enrollment code** from the owner (Dashboard → Sync → Add a helper device).
   3. Side panel → **Settings → Enroll**. Master URL: `https://abhishesh.tail66d6e3.ts.net:8443`. Enter the code.

## Daily use

1. On LinkedIn, run a **people search** with any filters.
2. Side panel → **Collect → LinkedIn page → Capture people on this page**.
3. Check the list: new people are pre-selected, and people the team already saved are marked. Click **Save**.
4. Go to the next results page on LinkedIn and capture again.

Everything is saved on your computer right away. It syncs to the team database whenever the master is reachable, even if you were offline. The **Sync** tab shows the status.

> LinkedIn's terms restrict tools that copy data from its pages, and LinkedIn can limit accounts that use them. Capture reads only what is on your screen, and only when you click. It never scrolls, pages or opens profiles for you.

## Updating

When the side panel shows **Update available**:

1. Download the new zips from the link above.
2. **Extension:** unzip over your extension folder (replace the files), then in `chrome://extensions` click the **reload** icon on Prospect Hub.
3. **Helper:** unzip over your helper folder, then run `node install-service.mjs --remove` followed by `node install-service.mjs`. Your data stays.

## Uninstall

- **Extension:** remove it in `chrome://extensions`.
- **Helper:** run `node install-service.mjs --remove`, then delete the folder. Local data is in `%LOCALAPPDATA%\ProspectHub\helper` (Windows) or `~/Library/Application Support/ProspectHub/helper` (Mac). Delete it only after the Sync tab shows nothing pending.
