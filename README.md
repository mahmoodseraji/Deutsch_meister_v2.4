# Deutsch Meister — Version 2.4

A professional, offline-first German vocabulary trainer PWA designed for iPhone and desktop.

## V2 features
- Preserves the V1 IndexedDB database name (`deutsch-meister-db`), version (`1`), and existing `words` and `settings` object stores. Existing vocabulary and review progress remain in place.
- Bottom navigation and responsive professional interface.
- Animated view transitions and flashcard entrance, respecting reduced-motion preferences.
- German pronunciation using the browser Web Speech API (`de-DE`), including vocabulary, example sentences, quiz prompts, and optional voice selection.
- Multiple-choice vocabulary quiz.
- Learning statistics, seven-day activity, daily goal progress, and vocabulary distribution.
- Favorites and category filtering.
- Dark mode.
- Manual vocabulary entry/edit/delete, CSV import/export, JSON backup/restore.
- Leitner and Anki-style SM-2 scheduling.

## Deploy
Upload the contents of this folder to the GitHub Pages branch/root used by your current site. Keep `index.html`, `styles.css`, `app.js`, `sw.js`, and `manifest.json` together. GitHub Pages must serve the site over HTTPS.

## Upgrade safely
1. Before deploying, open the V1 app and use **Import & backup → Export full backup (JSON)**.
2. Upload the V2 files over the V1 app files in the same GitHub Pages location.
3. Open the app online once so the new service worker can install and update the cache.
4. If the old interface remains visible, close the installed PWA completely and reopen it while online. The service worker cache name has changed to `deutsch-meister-v2.0.0`.
5. Confirm that your words and progress are present. Keep the JSON backup until verified.

The app intentionally does not change the IndexedDB database version or object-store schema. New word properties such as `favorite` are optional fields on existing word records, so no destructive migration is required.

## Run locally
From this folder run:

```bash
python -m http.server 8000
```

Then open `http://localhost:8000`.

## CSV format
Required columns: `german`, `translation`. Optional columns: `article`, `plural`, `example`, `notes`, `category`.

## Pronunciation note
Pronunciation uses `speechSynthesis` with the `de-DE` locale and a German voice available on the device. Voice availability, quality, and offline behaviour depend on the browser and installed system voices. On iPhone, test in Safari and after adding the site to the Home Screen.

## Backup reminder
Browser storage can be cleared by iOS or by clearing website data. Export JSON backups regularly and keep a copy outside the device.


## V2.3 — Motivation & progress

- Daily streaks: a day is earned after reviewing at least five words or completing a quiz.
- Current and longest streaks, plus a seven-day consistency calendar.
- The streak history starts from the first qualifying activity after installing V2.3. Older `lastReviewed` dates are not treated as verified streak days because V1/V2 did not retain complete daily activity history.
- Activity counts and streak dates are stored in the existing IndexedDB `settings` store. The database name, version, stores and existing vocabulary records are unchanged.
- Dashboard progress labels and visual hierarchy are clearer; the selected Leitner/SM-2 review method remains intact.

### Updating from V2.1
Export a JSON backup first. Replace the six project files in the GitHub Pages root with these V2.3 files, open the site online once, then fully close and reopen the installed PWA. The service-worker cache is versioned as `deutsch-meister-v2.3.0`.


### V2.3 fix
The Import & Backup screen is now reachable from Settings via the “Open Import & Backup” button. The screen also has a Back to Settings control. The CSV import and JSON restore handlers remain unchanged.


## V2.4 reliability fix
- CSV vocabulary import and all backup actions are displayed directly inside Settings; no separate hidden Tools screen is required.
- JSON export, JSON restore, CSV export, and sample CSV download have distinct, clearly labelled controls.
- File-picker inputs remain visually hidden but are full-size transparent overlays inside their labels, making the CSV/JSON chooser reliably tappable on touch devices.
- Added tactile press feedback, keyboard focus indication, and hover feedback to buttons and file controls.
- Service-worker cache version bumped to `deutsch-meister-v2.4.0`.
- IndexedDB database name/version/stores and existing vocabulary data format are unchanged.
