# AGENTS.md — lostinsanity.net

An archive site for **Lost in Sanity**, a two-piece band from Ludington,
Michigan, active roughly **July 2004 – February 2005**. Josh Mogerman on vocals
and drums, Brandon Martinez on guitar. Originally called **THEM**, renamed to
avoid a conflict with an eighties band.

This is an archive, not a working band page. Nothing is for sale and no address
is monitored.

## The domain is new — say so, don't imply otherwise

**Lost in Sanity never owned a domain.** The site lived as a folder on the
hosting account of Geeky Computer Services (Brandon's own business), which is
why every original page is stamped _"Copyright © 2004 Lost In Sanity & Geeky
Computer Services."_ When that hosting was cancelled on **2005-03-13**, the site
went with it. There is **no Internet Archive capture**.

`lostinsanity.net` was registered on **2026-07-31**, purely to host this archive.
`lostinsanity` was, historically, only a **PureVolume and GarageBand.com
username**, registered 2007-01-02 — after the band had already stopped. Never
write copy that suggests the band was at this address in 2004.

## The one rule: do not invent content

All quoted text is verbatim from the original site. Typos and grammar are
preserved ("Febuary 5th", "Jon Bonham", "Led Zepplin", "kickin' rifts", "I've
been having a lot of fun it"). **Do not fix them.**

Editorial voice is confined to section intros, the `#story` section, and the
archive banner.

## Provenance

| On the page          | Source                                                        |
| -------------------- | ------------------------------------------------------------- |
| Home page copy, THEM | `Lost in Sanity/main.html`                                    |
| 21 news posts        | `Lost in Sanity/news.html` (complete, nothing omitted)        |
| 15 journal entries   | `Lost in Sanity/brandon.html` (complete)                      |
| Bios and equipment   | `Lost in Sanity/bios.html`                                    |
| Track listings       | `Lost in Sanity/audio.html`                                   |
| Battle of the Bands  | `Lost in Sanity/other/battle.html`                            |
| Wallpapers           | `Lost in Sanity/wallpaper/` (3, made October 2004)            |
| Logo and bio photos  | `Lost in Sanity/img/`                                         |
| The EP audio         | `/Volumes/Audio/Personal Music Backup/Lost in Sanity/The Lost in Sanity EP/` |
| Demo audio           | Same volume, `Demos/`, plus `/Volumes/Audio/Logic/Archives/Lost in Sanity/Demo/` |
| `The Feast` (2008)   | `/Volumes/Audio/Logic/Archives/Lost in Sanity/The Feast/Bounces/The Feast.mp3` |
| "What came later" copy | The band's own account of the 2007-08 method, plus ID3 tags and dated jam folders |

Source ZIP: `~/src/_archive/Martinez Media/ZIP Backups/Lost in Sanity.zip`.
Extracted structured text: `data/site-export.json`.
Research writeup:
`brandonmartinez-secondbrain/02-Areas/Web Presence/Docs/2026-07-31 - Legacy Site & Band Archive Inventory.md`.

### Audio notes

- The EP is the original **128 kbps** master set, seven tracks including a hidden
  bonus track. Track 1's file is named **"Welcome to THEM"** — the pre-rename
  recording. The 2005 site listed that track as `UNAVAILABLE`; it is here.
- Demos are the raw session bounces at 128–320 kbps and are **not** re-encoded.
  `Never` appears on no release.
- **`When You're No Where You're Now Here` is NOT a Lost in Sanity song.** It is
  by **Josh Dumas**, a member of [blythe](https://blythe-band.com). It was in the
  same folder on disk and was mistakenly published here on 2026-07-31; removed
  the same day. Do not re-add it.
- The promised follow-up full-length ("The Lost in Sanity CD") was never made.
  **But the band did come back**, 2007-2008 - see below. Do not write copy
  saying they "stopped playing in 2005"; the *web site* stopped in 2005.

## The 2007-2008 era ("What came later")

Two years after the last news post the pair started recording again, onto an
iMac running Logic rather than the old multitrack recorder. Method, in Brandon's
words: hit record, jam for a while, cut the decent stuff up into an "album."
About **21 dated session folders** survive (`/Volumes/Audio/Logic/Archives/Lost
in Sanity/jams/`, 2007-05-20 through 2008-09-13, ~33 GB) and roughly a dozen
self-assembled records came out of them (658 MB, 122 files, in `Personal Music
Backup/Lost in Sanity/`).

**Only `The Feast` is published here so far.** 2:52, 320 kbps, bounced
2008-02-12 22:26 in Logic Pro 8.0.1; tagged *The Feast EP* track 1/3, key C,
120 BPM, "Heavy Rock"; composers Brandon Martinez and Josh Mogerman, lyrics
Josh Mogerman. Its ID3 `WXX` frame carries
`http://www.purevolume.com/lostinsanity`.

Rules for this section:

- **Do not claim a release or an audience.** Nothing from this era was announced
  anywhere we can cite. The PureVolume link in the file's tags is the only
  evidence anyone outside the room was meant to hear it, and we cannot prove
  which songs actually went up.
- The earlier 3:02 / 128 kbps version of the song (Logic Express 7.2.3, on *The
  Faces of Today EP*) is **not** the one to publish.
- Adding more of this era is a size question, not a taste one - it will not fit
  comfortably in the repo. See the Azure Blob staging note in the vault doc.

## Deliberately excluded — do not add these

- **The guestbook** and any visitor email addresses.
- **Band members' birth dates** (both were on the 2004 bios page; full name plus
  DOB plus hometown is an identity-theft triple).
- The `mailto:` addresses from the original site — the domain is not one we can
  receive mail on, and they were personal accounts.

## Regenerating

`src/index.html` is generated by `gen_lis.py` (kept in the session state folder)
from `data/site-export.json`. The file is hand-editable afterwards; if you
regenerate, re-apply any hand edits.

## Build

House pattern (see `Static Site Build & Deploy.md` in the vault):

```sh
npm install
npm run dev     # tailwind --watch + vite on :4175
npm run build   # → _site/
```

- Tailwind **v4**, no `tailwind.config.js`; theme in `@theme`.
- Exactly three dev dependencies plus the `shell-quote` override. **`npm audit`
  must report zero.**
- `src/` ships as-is; the build is `cp -R src/. _site/`. Vite is a dev server
  only.
- **No audio ships in this repo.** Every track streams from Azure Blob Storage at
  `https://martinezmediaclients.blob.core.windows.net/lostinsanity/`. The repo
  used to carry ~65 MB of MP3s; it is now 2.5 MB. Do not add audio files back.

## Audio & the player

Tracks live in blob storage under three prefixes: `albums/<year>-<slug>/`,
`masters/`, and `_excluded-covers/` (**never** referenced from the site). The
container is public at the **blob** access level, not container level, so the
archive cannot be enumerated by a stranger.

Each track on the page is an `<article class="track">` carrying its own data:

```html
<article class="track" data-src="<absolute blob URL>" data-title="Hangover Blues" data-seconds="177">
```

`src/player.js` collects those, wires one shared `Audio()` object, and drives a
sticky now-playing bar (`#player`). Rules:

- **A track's `data-seconds` must match the printed duration.** It is what the
  bar shows before metadata loads.
- Tracks are grouped into playlists by the nearest `[data-playlist]` ancestor;
  `data-record` on that element is the label shown in the bar. Auto-advance and
  prev/next stay **inside** one record.
- Player styles live in `@layer components` in `styles/tailwind.css`. Tailwind
  utilities always beat that layer regardless of specificity — so a state rule
  like `.track.is-active .track-title` only works if the element carries **no**
  competing utility (that is why track `<h3>`s have no `text-zinc-100`).
- `preload="none"` behaviour is intentional: nothing is fetched until a play
  button is pressed.

Before publishing, confirm every `data-src` resolves:

```sh
grep -o 'data-src="[^"]*"' _site/index.html | sed 's/data-src="//;s/"//' \
  | while read u; do echo "$(curl -sS -o /dev/null -w '%{http_code}' -I "$u") $u"; done
```

## Deploy

GitHub Pages via Actions, custom domain `lostinsanity.net`.

```sh
gh api -X PUT /repos/brandonmartinez/lostinsanity/pages -f build_type=workflow
```
