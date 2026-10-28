# Strava Activity Animator

A standalone browser app for importing and animating GPS activity history. Open `index.html` in a modern browser, or serve this repository with GitHub Pages.

## Use

1. Try the synthetic demo, or import TCX, GPX, FIT, GZ files or a Strava export ZIP.
2. Include the export's `activities.csv` to preserve original activity names and sport types.
3. Filter by UTC dates and sport, or search by activity name.
4. Play, pause, scrub, change speed, or choose route progress, elapsed time, time of day, or activity history playback.
5. Drag to pan, use the mouse wheel or +/− to zoom, and Fit routes to return to the collection.

## Privacy

Activity files are processed in memory in the browser and are never uploaded by this app. Refresh or Clear all removes them. No analytics, login, server database or activity persistence is included. The default No tiles mode works offline. Optional online street/satellite maps request the viewed map area from Esri; the provider also receives your IP address. Imported filenames and GPS data must never be committed to this repository.

## Compatibility and limits

- Modern Chrome, Edge, Firefox or Safari; GZ requires `DecompressionStream`.
- GPS routes need at least two valid coordinates. Indoor activities without GPS cannot appear on the map.
- FIT supports standard activity GPS record messages and compressed timestamps; exotic or non-activity FIT files may be rejected. FIT CRC is checked.
- Imports: 300 MB compressed/input total per batch, 100 MB per expanded ZIP entry, 500 MB expanded per batch, 20,000 route files. Use smaller batches for large exports.
- Dates and time-of-day playback use UTC. Activities continuing across midnight may extend beyond the time-of-day window. Missing timestamps use point order for animation and do not count towards recorded time.
- Distance is calculated from GPS points; totals may differ from Strava's corrected/moving-time statistics.
- The first 100 activity rows are listed; use search and filters to find others. All filtered routes remain on the map. Automatic rendering uses cached full-route backgrounds and moving positions above 250 activities, capped at 30 fps. Choose Animated trails for progressive trail drawing, or Fast to force the lighter view. Display geometry is reduced to a screen-space point budget; original GPS points and statistics are retained. Route bounds and playback extents are cached.
- ZIP extraction uses bundled JSZip 3.10.1, licensed under MIT; see `JSZip-LICENSE.txt` and the embedded license notice. No CDN is needed.
- Optional maps depend on the provider's availability and terms. This is independent software, not affiliated with Strava.

## GitHub Pages

In Settings → Pages, deploy from branch `main`, folder `/ (root)`. The entry point is `index.html`; no build is required.

## Validation

Synthetic checks covered TCX, GPX, GPX.GZ, ZIP/CSV metadata, FIT and checksum rejection, duplicate imports, zero coordinates, date filters, demo generation, all four animation calculations, escaped names and offline rendering. Live browser smoke checks verified demo rendering, playback, filters, zoom and shared starts. A synthetic performance regression check covered 1,000 activities / 1,000,000 GPS points with cache invalidation and all routes retained; its timing measurements exclude real browser painting. Real user export compatibility has not yet been validated.
