# SoulPulse content

Public files that the SoulPulse app downloads. No app code lives here.

## Verse library (`library/`)

The curated verses (references, focuses, Verse of the Day, subtitle,
context). The app checks `library/manifest.json` when it opens and downloads
`library/verse_library.json` only when the version is newer, after checking
its size and SHA-256 checksum.

How it gets here: the Google Sheet's **SoulPulse > Publish verse library**
menu saves the Sheet's Export tab as `source/export.csv`. That starts the
"Publish verse library" workflow, which checks every row and, if all is
well and something changed, updates `library/`. The result of each run
(new version, or the rows to fix) is in `status/last_publish.json`.

## Bible translations (release `bibles-v1`)

| File | Translation | Source |
|------|-------------|--------|
| `kjv.sqlite.gz` | King James Version | eBible.org `eng-kjv2006` |
| `bbe.sqlite.gz` | Bible in Basic English | eBible.org `engBBE` |

Both texts are in the public domain. Files are built by the app's
`tool/build_bibles.dart` script, and the app checks each download against a
SHA-256 checksum before using it. Release files are never replaced; changed
files go under a new release tag.
