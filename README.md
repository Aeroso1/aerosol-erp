# Aerosol ERP — downloads

A local, single-user personal ERP for macOS. One window, one SQLite database,
no account and no cloud service: tasks, calendar, habits, goals, checklists,
CRM, notes, water tracking and time-since trackers live on your Mac. Two-way
Apple Calendar (CalDAV) sync is the only network feature.

This repository holds **releases only**. It contains no source code and no
history — the source lives in a separate private repository.

## Download

Open the [Releases](../../releases/latest) page and download:

- `Aerosol-ERP-<version>-macos-arm64.zip`
- `SHA256SUMS`

Verify the download before opening it:

```bash
cd ~/Downloads
shasum -a 256 -c SHA256SUMS
```

Expected output ends with `OK`. If it does not, delete the download and ask for
a new copy.

## Install

1. Unzip and drag `Aerosol ERP.app` to `/Applications`.
2. **Right-click** (or Control-click) the app and choose **Open**, then **Open**
   again in the dialog. A plain double-click is blocked because the build is
   ad-hoc signed and not notarized; there is no Apple Developer ID behind 0.2.
3. The app creates `~/Library/Application Support/PersonalERP/` on first
   launch. There is no setup wizard.

Requires macOS 12 or newer on Apple Silicon.

## Privacy

No telemetry, no analytics, no crash reporter and no auto-update. Nothing is
sent anywhere unless you connect Apple Calendar, and then only to
`caldav.icloud.com`.

## Problems

Include the app version and schema from the app's `--diagnostics` output, your
macOS version, and the smallest log excerpt that shows the error. Diagnostics
contain no event titles, contacts, calendar names, URLs or credentials, and
paths are shown relative to your home directory.

**Never send your `personal_erp.db` or a backup** — they contain everything you
have entered.
