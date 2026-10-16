# Third-Party Notices

This file lists the third-party components Reels Downloader is built from and
redistributes, the licence each one is under, and where the licence text is.
It is installed with the application, beside this file in the application's
`resources\` folder.

Where a licence is not reproduced in full here, the full text is either shipped
with the component itself, shipped as a separate file in `resources\`, or both.

---

## 1. Reels Downloader itself

Copyright (c) 2026 Mohamed Farouk Amer. The application's own licence is
`LICENSE.txt`, shipped beside this file. It is the owner's proprietary notice:
**nothing** in it restricts any right granted by any of the licences below, and
none of those licences is modified or overridden by it.

## 2. FFmpeg

`ffmpeg.exe`, version `n9.0.2-24-gfd5d616c29-20261009`, statically linked x86_64
Windows build.

- **Licence:** GNU LGPL v2.1 or later, upgraded to version 3 by the build's
  `--enable-version3`. GPL-only parts are **not** enabled; no non-free library
  is enabled.
- **Copyright:** `Copyright (c) 2000-2026 the FFmpeg developers`.
- **Full notice:** `FFMPEG-COPYRIGHT-NOTICE.md` — build identification, the
  complete configuration line, and the linked external libraries.
- **Licence text:** `FFMPEG-LICENSE-LGPLv3.txt`, and `LICENSE-GPLv3.txt` for the
  GPL v3 text that LGPL v3 section 3 lets you elect.
- **Corresponding source:** `FFMPEG-SOURCE-OFFER.md` — the written offer LGPL v3
  section 6 requires, with the exact source commits, archive checksums, and
  instructions for replacing the binaries.
- **ffprobe:** the application conveys `ffmpeg.exe` only. Nothing it does spawns
  ffprobe — a merge of an AV1 video stream with an AAC audio stream completes
  without it — so no `ffprobe.exe` is shipped. The LGPL obligations above attach
  to the one binary that is conveyed.

## 3. yt-dlp

`yt-dlp.exe`, release **2026.08.19**.

- **Licence:** The Unlicense. yt-dlp's own statement: the executable is a
  PyInstaller bundle, and it is "subject to these and other licenses, all of
  which are compiled in THIRD_PARTY_LICENSES.txt" (yt-dlp release notes for
  2026.08.19).
- **Aggregated licence texts:** shipped beside this file as
  `YT-DLP-THIRD-PARTY-LICENSES.txt`, taken verbatim from the yt-dlp repository
  at the commit the release notes for 2026.08.19 cite.

Components bundled inside the PyInstaller executable, as listed by yt-dlp
itself for this release:

| Component | Licence |
|---|---|
| Python | PSF-2.0 |
| bzip2 | bzip2-1.0.6 |
| libffi | MIT |
| OpenSSL 3.0+ | Apache-2.0 |
| SQLite | Public Domain |
| liblzma | 0BSD |
| mpdecimal | BSD-2-Clause |
| zlib | zlib |
| Expat | MIT |
| brotli | MIT |
| mutagen | GPL-2.0-or-later |
| PyCryptodome | Public Domain and BSD-2-Clause |
| certifi | MPL-2.0 |
| requests | Apache-2.0 |
| charset-normalizer | MIT |
| idna | BSD-3-Clause |
| urllib3 | MIT |
| websockets | BSD-3-Clause |

**Note `mutagen`, which is GPL-2.0-or-later.** The list above is not this
project's reading of the bundle; it is the list yt-dlp publishes, fetched from
the upstream release page and its referenced `THIRD_PARTY_LICENSES.txt` for the
pinned version. Questions about the licensing of the yt-dlp bundle should be
directed upstream; the aggregated texts in
`YT-DLP-THIRD-PARTY-LICENSES.txt` are what yt-dlp says governs it.

## 4. Electron and Chromium

The application is an Electron **44.7.0** application.

- **Electron** is MIT licensed. Its licence text is installed at the
  application's install root as `LICENSE.electron.txt` (1,096 bytes).
- **Chromium** is BSD-style licensed with the third-party notices kept by the
  upstream project. Its complete third-party notice file is installed at the
  application's install root as `LICENSES.chromium.html` (20,477,229 bytes),
  and it enumerates **778** third-party components with their licence texts —
  among them FFmpeg, zlib, OpenSSL, libjpeg-turbo, ICU, Skia, and the many
  others Chromium is built from. That file is authoritative; nothing here
  summarises or re-derives it.
- The exact Chromium revision is not recorded in the installed licence files.
  The running application reports it as the Chrome version on its About
  information, and it is determined entirely by the pinned Electron version.

## 5. npm production dependencies

Every package in the application's production dependency tree, as reported by
`npm ls --omit=dev --all`. Compile-time-only packages (the `@types/*` type
definitions) are not included: they are not compiled into the application.
Optional peer dependencies that are not installed (`immer`,
`use-sync-external-store`) are not listed.

| Package | Version | Licence | Licence file shipped with the package |
|---|---|---|---|
| `@floating-ui/core` | 1.8.0 | MIT | LICENSE |
| `@floating-ui/dom` | 1.8.0 | MIT | LICENSE |
| `@floating-ui/react-dom` | 2.1.9 | MIT | LICENSE |
| `@floating-ui/utils` | 0.2.12 | MIT | LICENSE |
| `@radix-ui/colors` | 3.0.0 | MIT | LICENSE |
| `@radix-ui/number` | 1.1.3 | MIT | LICENSE |
| `@radix-ui/primitive` | 1.1.7 | MIT | LICENSE |
| `@radix-ui/react-accessible-icon` | 1.1.16 | MIT | LICENSE |
| `@radix-ui/react-accordion` | 1.2.21 | MIT | LICENSE |
| `@radix-ui/react-alert-dialog` | 1.1.24 | MIT | LICENSE |
| `@radix-ui/react-arrow` | 1.1.16 | MIT | LICENSE |
| `@radix-ui/react-aspect-ratio` | 1.1.16 | MIT | LICENSE |
| `@radix-ui/react-avatar` | 1.2.7 | MIT | LICENSE |
| `@radix-ui/react-checkbox` | 1.3.12 | MIT | LICENSE |
| `@radix-ui/react-collapsible` | 1.1.21 | MIT | LICENSE |
| `@radix-ui/react-collection` | 1.1.16 | MIT | LICENSE |
| `@radix-ui/react-compose-refs` | 1.1.5 | MIT | LICENSE |
| `@radix-ui/react-context` | 1.2.2 | MIT | LICENSE |
| `@radix-ui/react-context-menu` | 2.3.8 | MIT | LICENSE |
| `@radix-ui/react-dialog` | 1.2.0 | MIT | LICENSE |
| `@radix-ui/react-direction` | 1.1.5 | MIT | LICENSE |
| `@radix-ui/react-dismissable-layer` | 1.1.20 | MIT | LICENSE |
| `@radix-ui/react-dropdown-menu` | 2.1.25 | MIT | LICENSE |
| `@radix-ui/react-focus-guards` | 1.1.6 | MIT | LICENSE |
| `@radix-ui/react-focus-scope` | 1.2.0 | MIT | LICENSE |
| `@radix-ui/react-form` | 0.2.0 | MIT | LICENSE |
| `@radix-ui/react-hover-card` | 1.1.24 | MIT | LICENSE |
| `@radix-ui/react-id` | 1.1.4 | MIT | LICENSE |
| `@radix-ui/react-label` | 2.1.16 | MIT | LICENSE |
| `@radix-ui/react-menu` | 2.1.25 | MIT | LICENSE |
| `@radix-ui/react-menubar` | 1.1.25 | MIT | LICENSE |
| `@radix-ui/react-navigation-menu` | 1.3.0 | MIT | LICENSE |
| `@radix-ui/react-one-time-password-field` | 0.1.17 | MIT | LICENSE |
| `@radix-ui/react-password-toggle-field` | 0.1.12 | MIT | LICENSE |
| `@radix-ui/react-popover` | 1.2.0 | MIT | LICENSE |
| `@radix-ui/react-popper` | 1.3.8 | MIT | LICENSE |
| `@radix-ui/react-portal` | 1.1.18 | MIT | LICENSE |
| `@radix-ui/react-presence` | 1.1.11 | MIT | LICENSE |
| `@radix-ui/react-primitive` | 2.1.11 | MIT | LICENSE |
| `@radix-ui/react-progress` | 1.1.17 | MIT | LICENSE |
| `@radix-ui/react-radio-group` | 1.4.8 | MIT | LICENSE |
| `@radix-ui/react-roving-focus` | 1.1.20 | MIT | LICENSE |
| `@radix-ui/react-scroll-area` | 1.3.0 | MIT | LICENSE |
| `@radix-ui/react-select` | 2.3.8 | MIT | LICENSE |
| `@radix-ui/react-separator` | 1.1.16 | MIT | LICENSE |
| `@radix-ui/react-slider` | 1.5.0 | MIT | LICENSE |
| `@radix-ui/react-slot` | 1.4.0 | MIT | LICENSE |
| `@radix-ui/react-switch` | 1.3.8 | MIT | LICENSE |
| `@radix-ui/react-tabs` | 1.1.22 | MIT | LICENSE |
| `@radix-ui/react-toast` | 1.2.24 | MIT | LICENSE |
| `@radix-ui/react-toggle` | 1.1.19 | MIT | LICENSE |
| `@radix-ui/react-toggle-group` | 1.1.20 | MIT | LICENSE |
| `@radix-ui/react-toolbar` | 1.1.20 | MIT | LICENSE |
| `@radix-ui/react-tooltip` | 1.3.0 | MIT | LICENSE |
| `@radix-ui/react-use-callback-ref` | 1.1.4 | MIT | LICENSE |
| `@radix-ui/react-use-controllable-state` | 1.2.6 | MIT | LICENSE |
| `@radix-ui/react-use-effect-event` | 0.0.5 | MIT | LICENSE |
| `@radix-ui/react-use-escape-keydown` | 1.1.5 | MIT | LICENSE |
| `@radix-ui/react-use-is-hydrated` | 0.1.3 | MIT | LICENSE |
| `@radix-ui/react-use-layout-effect` | 1.1.4 | MIT | LICENSE |
| `@radix-ui/react-use-previous` | 1.1.4 | MIT | LICENSE |
| `@radix-ui/react-use-rect` | 1.1.4 | MIT | LICENSE |
| `@radix-ui/react-use-size` | 1.1.5 | MIT | LICENSE |
| `@radix-ui/react-visually-hidden` | 1.2.12 | MIT | LICENSE |
| `@radix-ui/rect` | 1.1.3 | MIT | LICENSE |
| `@radix-ui/themes` | 3.3.0 | MIT | LICENSE |
| `ajv` | 8.20.0 | MIT | LICENSE |
| `ajv-formats` | 3.0.1 | MIT | LICENSE |
| `aria-hidden` | 1.2.6 | MIT | LICENSE |
| `argparse` | 2.0.1 | Python-2.0 | LICENSE |
| `atomically` | 2.1.1 | MIT | license |
| `builder-util-runtime` | 9.7.0 | MIT | LICENSE |
| `classnames` | 2.5.1 | MIT | LICENSE |
| `conf` | 15.1.0 | MIT | license |
| `csstype` | 3.2.3 | MIT | LICENSE |
| `debug` | 4.4.3 | MIT | LICENSE |
| `debounce-fn` | 6.0.0 | MIT | license |
| `detect-node-es` | 1.1.0 | MIT | LICENSE |
| `dot-prop` | 10.2.0 | MIT | license |
| `electron-store` | 11.0.2 | MIT | license |
| `electron-updater` | 6.8.10 | MIT | LICENSE |
| `env-paths` | 3.0.0 | MIT | license |
| `fast-deep-equal` | 3.1.3 | MIT | LICENSE |
| `fast-uri` | 3.1.8 | BSD-3-Clause | LICENSE |
| `fs-extra` | 10.1.0 | MIT | LICENSE |
| `get-nonce` | 1.0.1 | MIT | LICENSE |
| `graceful-fs` | 4.2.11 | ISC | LICENSE |
| `json-schema-traverse` | 1.0.0 | MIT | LICENSE |
| `json-schema-typed` | 8.0.2 | BSD-2-Clause | LICENSE.md |
| `js-yaml` | 4.3.2 | MIT | LICENSE |
| `lazy-val` | 1.0.5 | MIT | **none** |
| `lodash.escaperegexp` | 4.1.2 | MIT | LICENSE |
| `lodash.isequal` | 4.5.0 | MIT | LICENSE |
| `lucide-react` | 1.54.0 | ISC | LICENSE |
| `mimic-function` | 5.0.1 | MIT | license |
| `ms` | 2.1.3 | MIT | license.md |
| `radix-ui` | 1.7.0 | MIT | LICENSE |
| `react` | 19.3.0 | MIT | LICENSE |
| `react-dom` | 19.3.0 | MIT | LICENSE |
| `react-remove-scroll` | 2.7.2 | MIT | LICENSE |
| `react-remove-scroll-bar` | 2.3.8 | MIT | **none** |
| `react-style-singleton` | 2.2.3 | MIT | LICENSE |
| `require-from-string` | 2.0.2 | MIT | license |
| `scheduler` | 0.28.0 | MIT | LICENSE |
| `semver` | 7.8.5 | ISC | LICENSE |
| `semver` (nested under `electron-updater`) | 7.7.4 | ISC | LICENSE |
| `stubborn-fs` | 2.0.0 | MIT | license |
| `stubborn-utils` | 1.0.2 | MIT | license |
| `tagged-tag` | 1.0.0 | MIT | license |
| `tiny-typed-emitter` | 2.1.0 | MIT | LICENSE |
| `tslib` | 2.8.1 | 0BSD | CopyrightNotice.txt, LICENSE.txt |
| `type-fest` | 0.13.1 | (MIT OR CC0-1.0) | license |
| `uint8array-extras` | 1.6.0 | MIT | license |
| `universalify` | 2.0.1 | MIT | LICENSE |
| `use-callback-ref` | 1.3.3 | MIT | LICENSE |
| `use-sidecar` | 1.1.3 | MIT | LICENSE |
| `when-exit` | 2.1.5 | MIT | license |
| `zod` | 4.6.5 | MIT | LICENSE |
| `zustand` | 5.0.15 | MIT | LICENSE |

**Flagged: `react-remove-scroll-bar` 2.3.8 ships no licence file.** Its
`package.json` declares the MIT licence, and MIT's terms apply to it regardless,
but the project distributes no copy of the licence text with the package. The
parent package `react-remove-scroll` (2.7.2, MIT) does ship `LICENSE`. The MIT
text is a short standard licence; it is not reproduced in this folder, and can be
read at `https://opensource.org/license/mit`.

**Flagged: `lazy-val` 1.0.5 ships no licence file.** Same situation: its
`package.json` declares MIT, MIT's terms apply regardless, and no licence text is
distributed with the package.

**Note on `sax` 1.6.1.** It is declared under the Blue Oak Model License 1.0.0,
a permissive licence. It reaches the production tree through
`electron-updater` (via `builder-util-runtime`), which parses XML update
metadata.

## 6. Files installed beside this one

| File | Contents |
|---|---|
| `LICENSE.txt` | The application's own licence: the owner's proprietary notice for the developer-owned portions |
| `THIRD_PARTY_NOTICES.md` | This file |
| `FFMPEG-LICENSE-LGPLv3.txt` | GNU LGPL v3 text |
| `LICENSE-GPLv3.txt` | GNU GPL v3 text |
| `FFMPEG-COPYRIGHT-NOTICE.md` | FFmpeg copyright and licence notice |
| `FFMPEG-SOURCE-OFFER.md` | Written offer of FFmpeg corresponding source |
| `YT-DLP-THIRD-PARTY-LICENSES.txt` | Licence texts of the components bundled into `yt-dlp.exe` |
| `FFMPEG-SHA256SUMS.txt` | SHA-256 of the FFmpeg binaries, as verified at fetch time |
| `SHA2-256SUMS` | yt-dlp's own release manifest for 2026.08.19 |
