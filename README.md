# Aerosol ERP

A local, single-user personal ERP for macOS. Tasks, calendar, habits, goals,
checklists, contacts, notes, water tracking and time-since trackers in one
window, backed by one SQLite database on your Mac. No account, no subscription
and no cloud service. Two-way Apple Calendar sync is the only network feature.

**Current release: 0.2** · macOS 12 or newer · Apple Silicon (M-series)

> 0.2 is an early release. Back up your data (section 8) before you rely on it.

This repository contains **downloads only** — no source code.

## Quick start

1. Download the newest release from **[Releases](https://github.com/Aeroso1/aerosol-erp/releases)**.
2. Verify it (section 3), unzip, and drag the app into **Applications**.
3. Right-click the app → **Open** → **Open**.

That is the whole setup. The app creates its database on first launch.

## 1. Check your Mac

- **Apple Silicon** (M1, M2, M3, M4): Apple menu → **About This Mac** → **Chip**
  must start with "Apple". Intel Macs cannot run this build.
- **macOS 12 Monterey or newer.**
- About 100 MB of free disk space.
- No Python installation is needed.

## 2. Download

Open **https://github.com/Aeroso1/aerosol-erp/releases** and choose the newest
release at the top. Download both files:

- `Aerosol-ERP-<version>-macos-arm64.zip` — the app (about 21 MB)
- `SHA256SUMS` — checksums for the download

Keep both files in the same folder (normally `~/Downloads`).

## 3. Verify the download

This confirms the file is complete and unmodified. Open **Terminal** and run:

```bash
cd ~/Downloads
shasum -a 256 -c SHA256SUMS
```

Expected output: one line per file, ending in `OK`.

If it says `FAILED`, delete the zip and download it again.

## 4. Install

1. Double-click the zip to unzip it.
2. Drag **Aerosol ERP.app** into your **Applications** folder.
3. Delete the zip (optional).

## 5. First launch

macOS blocks apps that are not notarized by Apple. This build is ad-hoc signed,
so the first launch needs one extra step:

1. Open **Applications** in Finder.
2. **Right-click** (or Control-click) **Aerosol ERP** and choose **Open**.
3. Click **Open** in the dialog.

After that, a normal double-click works.

If macOS says *"Aerosol ERP is damaged and can't be opened"*, run:

```bash
xattr -dr com.apple.quarantine "/Applications/Aerosol ERP.app"
open "/Applications/Aerosol ERP.app"
```

Only do this after the checksum in section 3 says `OK`.

## 6. Start using it

There is no sign-up, no licence key and no setup wizard. On first launch the
app creates its database and opens the dashboard. Everything stays on your Mac.

## 7. Where your data lives

```
~/Library/Application Support/PersonalERP/
├── personal_erp.db     your data (one SQLite file)
├── personal_erp.log    app log
├── backups/            automatic backups
└── .instance.lock      stops two copies running at once
```

- Do not move or delete this folder while the app is running.
- Do not put it in iCloud Drive, Dropbox or Google Drive.
- The folder is private to your macOS user account (mode `0700`).

## 8. Back up and restore

**Automatic:** the app writes one backup per day to `backups/` and keeps the
last 10. It also writes a backup before any database upgrade.

**Manual:** quit the app (⌘Q), then copy `personal_erp.db` somewhere safe.

**Restore:**

1. Quit the app.
2. Open `~/Library/Application Support/PersonalERP/backups` in Finder
   (**Go → Go to Folder**, paste the path).
3. Keep a copy of the current `personal_erp.db`, then replace it with the
   backup you want, renamed to `personal_erp.db`.
4. Relaunch the app.

## 9. Update

1. Quit the app.
2. Download and verify the new release (sections 2–3).
3. Replace **Aerosol ERP.app** in Applications.
4. Open it normally.

Your data stays where it is. If the database format changed, the app upgrades
it automatically and writes a backup first.

## 10. Uninstall

1. Quit the app.
2. Drag **Aerosol ERP.app** from Applications to the Trash.
3. Optional — this deletes all your data:

   ```bash
   rm -rf ~/Library/Application\ Support/PersonalERP
   ```

## 11. Troubleshooting

| Symptom | What to do |
|---|---|
| "Apple could not verify…" | Right-click the app → **Open** → **Open** (section 5) |
| "…is damaged and can't be opened" | Check the checksum, then run the `xattr` command in section 5 |
| Nothing opens, or no second window | Only one copy can run. Quit any other Aerosol ERP process, then reopen |
| App will not start after an update | Restore the newest backup (section 8) |
| Apple Calendar will not connect | Use an **app-specific password** from appleid.apple.com → Sign-In and Security → App-Specific Passwords. Your normal Apple ID password will not work |

## 12. Privacy

- No telemetry, analytics, crash reporting or auto-update.
- Nothing is sent anywhere unless you connect Apple Calendar, and then only to
  `caldav.icloud.com`.
- The calendar password is stored in your macOS Keychain, not in the database.

## 13. Getting help

Open an issue: **https://github.com/Aeroso1/aerosol-erp/issues**

Please include the output of:

```bash
"/Applications/Aerosol ERP.app/Contents/MacOS/Aerosol ERP" --version
"/Applications/Aerosol ERP.app/Contents/MacOS/Aerosol ERP" --diagnostics
```

plus your macOS version and what you were doing when it went wrong.

The diagnostics output contains no event titles, contacts, calendar names, URLs
or credentials.

**Never attach `personal_erp.db` or a backup** — it contains everything you
have entered.

## Terms

Provided as-is, without warranty of any kind. Back up your data. Please ask
before redistributing the app.
