# Changelog

This is the public changelog for Reels Downloader. It records what each release
contains, and the versions of the tools each release bundles.

The development log - which records defects, investigations, and fixes rather
than releases - is kept with the project's engineering reports.
Engineering reports are maintained locally and are not included in the public
repository.

## 0.1.5

**Date:** 2026-10-19

**Bundled tools:**

| Component | Version |
|---|---|
| yt-dlp | 2026.08.19 |
| FFmpeg | n9.0.2-24-gfd5d616c29-20261009 |
| Electron | 44.7.0 |

### Summary

Adds regular Facebook video links and a real audio-only MP3 download, and makes
the project's local statistics dashboard start with a documented command.

- **Regular Facebook videos, not only Reels.** The link field now accepts the
  shapes Facebook's own share menu produces for an ordinary video —
  `/watch?v=<number>`, `/video.php?v=<number>`,
  `/<account>/videos/<number>`, `/<account>/videos/<slug>/<number>` and
  `/share/v/<token>` — on the same four Facebook hosts, in addition to the Reel
  shapes. A regular video reaches the same analysis, quality listing and
  download path as a Reel. Each accepted link is rebuilt into one canonical
  form from the validated numeric id alone, so tracking tags and other query
  parameters never survive into the request; a link that names no single video,
  or that carries two different ids, is refused rather than guessed at.
- **Audio-only MP3, on every platform.** The quality list for a download now
  ends with an **MP3 audio only** choice — on Facebook, YouTube (videos and
  Shorts), Instagram and TikTok, wherever the page offers downloadable media at
  all. Choosing it fetches the best available audio and converts it to MP3 with
  the bundled FFmpeg; the finished file is named `<id>.mp3` and is verified on
  disk like every other download. The choice is a reserved application-level
  entry, not a format id the interface supplies, so the interface can never
  name an audio format, a quality or an FFmpeg option. Every existing video
  quality, and the merge behaviour for video-only renditions, is unchanged.
- **The local statistics dashboard starts with a documented command.** The
  operator dashboard — a local administrative tool, not part of the installed
  application — is started with `npm run analytics:dashboard`, and it now
  reports a missing administrative token, an invalid port, or a port that is
  already in use with a clear message instead of a connection that is silently
  refused.

### Known issues

- **The installer is not code-signed.** Windows SmartScreen will warn about an
  unknown publisher. The release page publishes the installer's SHA-256; verify
  it before running the file. See `SECURITY.md`.
- **One LGPL question is the owner's to close.** The FFmpeg build is static, and
  the written offer discharges what it can by documentation; the residual
  section 4 question for a static build still needs the owner's own legal
  sign-off before redistribution. See `FFMPEG-SOURCE-OFFER.md`.
- **The new link shapes and the MP3 conversion are verified offline, not
  against live pages.** The Facebook regular-video shapes, the canonicalisation
  and the MP3 extraction command are covered by the offline test suite; no live
  public link on any platform was downloaded as part of this release, so a
  change on a platform's side could still affect a real run.
- **A platform can break this at any time.** The application reads public pages
  from Facebook, YouTube, Instagram and TikTok. A change on any platform's side
  can stop analysis or downloading for that platform without notice.

## 0.1.4

**Date:** 2026-10-19

**Bundled tools:**

| Component | Version |
|---|---|
| yt-dlp | 2026.08.19 |
| FFmpeg | n9.0.2-24-gfd5d616c29-20261009 |
| Electron | 44.7.0 |

### Summary

Makes the anonymous installation count run automatically, and removes the
Settings control for it. No platform's analysis or download behaviour changed.

- **The anonymous installation count now runs in the background.** It starts
  by itself on every launch — one small heartbeat at startup, then one every
  thirty minutes — for both new installations and upgrades, and there is no
  longer any switch to turn it on or off. A heartbeat is unchanged: a random
  identifier created on this computer, the application version, the operating
  system, and a schema version. No name, no phone number, no email address, no
  link, no file name, and no download history. What it reveals — an IP address
  to the project's own statistics service — is now what the privacy notice says
  it reveals.
- **The "Anonymous usage statistics" card is gone from Settings.** The switch,
  its title, its help text and its disclosure are removed, because there is no
  longer a control behind them. What the count does, and that it cannot be
  turned off, is stated in the privacy notice in `README.md` and
  `SECURITY.md` instead. An installation upgrading from 0.1.3 keeps every other
  setting it had, whatever that switch was left at.

### Known issues

- **The installer is not code-signed.** Windows SmartScreen will warn about an
  unknown publisher. The release page publishes the installer's SHA-256; verify
  it before running the file. See `SECURITY.md`.
- **The anonymous count cannot be disabled from the interface.** It runs in the
  background like the mandatory update check; the only way to stop the
  heartbeat is to block the statistics host or stop running the application.
  This is stated plainly in the privacy notice rather than left implicit.
- **A platform can break this at any time.** The application reads public pages
  from Facebook, YouTube, Instagram and TikTok. A change on any platform's side
  can stop analysis or downloading for that platform without notice.

## 0.1.3

**Date:** 2026-10-19

**Bundled tools:**

| Component | Version |
|---|---|
| yt-dlp | 2026.08.19 |
| FFmpeg | n9.0.2-24-gfd5d616c29-20261009 |
| Electron | 44.7.0 |

### Summary

Adds one support contact and hardens the code that ships. No platform's
analysis or download behaviour changed.

- **WhatsApp support.** The Settings page carries a labelled **WhatsApp
  Support** button. It opens the project's WhatsApp chat in the system browser
  through the application's existing external-link path: the address is a
  constant in the main process, it is re-checked against its own allowlist
  (https, the `wa.me` host, the exact support number, the default port, nothing
  appended) before the operating system is asked to open it, and nothing is
  loaded inside the application window. The renderer is never given a URL to
  name.
- **The shipped JavaScript is obfuscated.** The application's own compiled
  bundles are obfuscated at build time with `javascript-obfuscator`, a build-only
  dependency that is not itself shipped. Source maps were already absent and
  remain absent; the bundled tools, the licence and notice documents, the
  packaged dependencies, and the HTML and CSS are deliberately left readable
  because they must be.
- **Two stricter window settings, and one application-level rule.** Web dialogs
  (`alert`, `confirm`, `prompt`) are disabled outright — the interface uses none
  of them — and a page can no longer resize the window by requesting HTML
  fullscreen. Window creation is additionally denied at the application level for
  every web contents the process creates, not only for the application's own
  window. `contextIsolation`, the sandbox, the preload bridge, IPC validation and
  the navigation restrictions are unchanged.

### Known issues

- **Obfuscation is not a security boundary.** It makes the shipped code tedious
  to read; it does not prevent recovery. Packaged Electron code can still be
  extracted and understood by a determined analyst. Nothing here is a substitute
  for the integrity controls the installer already carries.
- **The installer is not code-signed.** Windows SmartScreen will warn about an
  unknown publisher. The release page publishes the installer's SHA-256; verify
  it before running the file. See `SECURITY.md`.
- **A platform can break this at any time.** The application reads public pages
  from Facebook, YouTube, Instagram and TikTok. A change on any platform's side
  can stop analysis or downloading for that platform without notice.

## 0.1.2

**Date:** 2026-10-19

**Bundled tools:**

| Component | Version |
|---|---|
| yt-dlp | 2026.08.19 |
| FFmpeg | n9.0.2-24-gfd5d616c29-20261009 |
| Electron | 44.7.0 |

### Summary

Fixes two defects found after 0.1.1. No platform's analysis or download
behaviour changed.

- **Thumbnails on YouTube, Instagram and TikTok.** The picture shown beside an
  analysis was only ever fetched from Facebook's image host, so an analysis on
  any other platform fell back to the neutral placeholder. The main-process
  fetch now accepts each supported platform's image family — Facebook,
  Instagram, YouTube and TikTok — while keeping the same rules it had before:
  https only, the default port only, a real host under one of those families,
  every redirect re-checked, and only a small local `data:` image handed to the
  renderer. The production Content-Security-Policy is unchanged.
- **The required-update window is now visible.** When an update is mandatory,
  it is shown in a window of its own, and that window was created hidden and
  never shown — so the check, the download, its progress, and any failure ran
  with nothing on screen, leaving the application blocked behind an invisible
  window with no Retry and no manual-download link. The window now shows itself
  as soon as its page has painted, so the version, the percentage, the
  transferred and total bytes, the download speed and the Retry and
  manual-download controls are all visible while the gate is pending. The
  progress shown is still the real figure reported by the downloader; nothing is
  estimated.

### Known issues

- **The updater-window fix reaches a running 0.1.1 only after it updates.**
  The 0.1.1 release contains the hidden window, so the one update a 0.1.1
  installation is offered — this one — is shown in the window it already has.
  From 0.1.2 onward the window is visible. This is recorded so the behaviour of
  that single transition is not reported as a new defect.
- **The installer is not code-signed.** Windows SmartScreen will warn about an
  unknown publisher. The release page publishes the installer's SHA-256; verify
  it before running the file. See `SECURITY.md`.
- **One LGPL question is the owner's to close.** The FFmpeg build is static, and
  the written offer discharges what it can by documentation; the residual
  section 4 question for a static build still needs the owner's own legal
  sign-off before redistribution. See `FFMPEG-SOURCE-OFFER.md`.
- **A platform can break this at any time.** The application reads public pages
  from Facebook, YouTube, Instagram and TikTok. A change on any platform's side
  can stop analysis or downloading for that platform without notice. A platform
  that moves its images to a different host family will also stop showing that
  platform's thumbnail until the fetch's allowlist is extended.

## 0.1.1

**Date:** 2026-10-19

**Bundled tools:**

| Component | Version |
|---|---|
| yt-dlp | 2026.08.19 |
| FFmpeg | n9.0.2-24-gfd5d616c29-20261009 |
| Electron | 44.7.0 |

### Summary

Adds two more supported platforms and a default download folder that persists
between runs. The Facebook behaviour described for 0.1.0 is unchanged.

- **YouTube downloads.** Paste a YouTube video or Shorts link; the application
  reads the page, lists the formats it offers together with the audio and video
  streams each one carries, and downloads the chosen one. A video-only quality
  is merged with its audio by the bundled FFmpeg, and the size estimate for a
  merged download accounts for both streams.
- **Instagram Reels.** Paste a public Instagram Reel link; the application reads
  the page and downloads the chosen quality through the same analysis, download
  and verification path as Facebook.
- **TikTok.** Paste a public TikTok video link; the application reads the page
  and downloads the chosen quality through the same path.
- **A persistent default download folder.** Choose a folder once in Settings and
  every download uses it. A folder picked for a single download still wins, and
  with no folder chosen the Download button stays disabled rather than writing
  somewhere the user did not name.
- **One download flow for every platform.** Analysis, quality listing, progress,
  cancel, already-downloaded detection and post-download verification behave the
  same on every supported platform; only the link field and the platform's own
  section change.

### Known issues

- **The installer is not code-signed.** Windows SmartScreen will warn about an
  unknown publisher. The release page publishes the installer's SHA-256; verify
  it before running the file. See `SECURITY.md`.
- **One LGPL question is the owner's to close.** The FFmpeg build is static, and
  the written offer discharges what it can by documentation; the residual
  section 4 question for a static build still needs the owner's own legal
  sign-off before redistribution. See `FFMPEG-SOURCE-OFFER.md`.
- **A platform can break this at any time.** The application reads public pages
  from Facebook, YouTube, Instagram and TikTok. A change on any platform's side
  can stop analysis or downloading for that platform without notice.

## 0.1.0

**Date:** 2026-10-16

**Bundled tools:**

| Component | Version |
|---|---|
| yt-dlp | 2026.08.19 |
| FFmpeg | n9.0.2-24-gfd5d616c29-20261009 |
| Electron | 44.7.0 |

### Summary

The first release. Everything here is new, so this is a description of the
application rather than a list of changes against an earlier version.

- **Analysis and download.** Paste a Facebook Reel link; the application reads
  the page and lists the qualities it offers, then downloads the one you choose.
  Progressive qualities arrive as one file; video-only qualities are merged with
  their audio stream by the bundled FFmpeg.
- **Supported links.** `facebook.com/reel/<id>`, `facebook.com/reels/<id>` and
  `facebook.com/share/r/<token>`, on the hosts `facebook.com`,
  `www.facebook.com`, `m.facebook.com` and `web.facebook.com`. Every other host
  and path shape is refused.
- **`fb.watch` short links are recognised but refused.** The link field reports
  that such a link looks valid, and the analysis then explains that the
  application will not follow a short-link redirect and asks for the Reel's
  permalink instead. No request is made to resolve the short link, which is the
  point: a redirect would take the application to a page it has not allowed.
- **No account.** The application sends no credentials and no cookies, and has
  no way to hold a login. If a page requires an account, the download fails
  rather than asking you to sign in.
- **Downloads are verified.** A run that reports success is checked against the
  file it was supposed to produce. If the merged result is missing — which
  happens when a component of the application has been removed — the download is
  reported as incomplete, the unusable intermediate files are cleared up, and
  the message tells you to reinstall rather than to try again.
- **Launch-time tool check.** The bundled tools are checked when the
  application starts. A missing or unresponsive download engine disables
  analysis and download with a clear warning; a missing merge tool only warns,
  because progressive qualities still work.
- **Already-downloaded detection.** Downloading the same Reel twice into the
  same folder reports that the file is already there instead of downloading it
  again or silently overwriting it.
- **Languages.** English and Arabic, with correct bidirectional layout in the
  Arabic interface.
- **The action bar is the page's footer.** Choose folder, Download and Cancel sit
  in a bar with the same padding and the same centred measure as the content
  above it, so their edges line up with the cards' at every window size. Below
  640px the bar becomes two rows: the chosen folder on one, the three buttons
  sharing the other. The download's progress — the bar, the numbers, and what is
  happening — now sits in the results panel, directly under the quality it
  describes, where the eye already is; the bar below holds nothing but buttons and
  a folder path.
- **A preview picture that cannot eat the panel.** The Reel's picture is a fixed
  9:16 frame capped at 320px tall or 40% of the window, whichever is smaller, so a
  tall window and a short one both get a thumbnail and a card that is exactly as
  tall as its content.
- **Accessibility.** Keyboard-navigable throughout, with contrast measured and
  passing AA on every sampled control in both themes.
- **Offline by design, network by necessity.** The application makes only the
  connections described in `release-docs/README.releases.md`: Facebook's public
  pages, and GitHub for the launch-time update check. Requests are
  HTTPS-only, certificate-validated, host-allowlisted, and they do not follow
  redirects to other hosts.

### Mandatory updates

- **The application updates before it opens.** On launch, before any window, the
  application asks GitHub whether a newer release exists. Up to date, it opens;
  a newer version is downloaded, installed, and the application restarts at the
  new version. There is no "continue anyway": Facebook changes its pages
  constantly, and a tool that cannot be updated is a tool that stops working.
- **A check that cannot be answered is not a block.** If the check fails or
  takes longer than twenty seconds, the application opens with a persistent
  warning banner — no newer version was confirmed, so blocking would punish the
  user for a condition the application cannot act on. A newer version that was
  confirmed but could not be installed *does* block, with Retry and a
  "Download manually" link to the releases page.
- **The updater is network-confined.** Every request the update component makes
  passes a deny-by-default policy: three GitHub hosts over HTTPS on the standard
  port, and nothing else. Other hosts, subdomains of the allowed ones, other
  schemes, and other ports are cancelled before they leave the process.
- **Verified end to end against a localhost feed.** The update path is tested
  with two test builds served over `http://127.0.0.1`: the update flow, a failed
  check, a hash mismatch, a downgrade refusal, and the single-instance lock. The
  localhost exception is a compile-time constant that is absent from every
  normal build, which the test suite asserts against the built bundle and the
  shipped `app.asar`.

### Progress, preview and control

- **The download bar reports the download.** Percent, bytes so far, transfer
  rate, and time remaining, with a separate stage for a merged download's video,
  audio and merge. Every measurement that is not yet known shows a dash and the
  bar goes indeterminate rather than inventing a number — a bar that lies about
  how far along it is is worse than one that admits it cannot tell.
- **Downloads can be stopped.** A Cancel button ends the transfer, removes the
  partial file this run created, and leaves everything else alone. It is not
  reported as an error and offers no remedy, because nothing went wrong.
- **Reels show a preview picture.** The picture is fetched by the application
  itself, from Facebook's image servers only, and handed to the interface as a
  small local copy. The original address never reaches the interface, which is
  also why the content-security policy no longer allows images from any remote
  host. A Reel with no picture shows a neutral placeholder.
- **The window opens at a size that fits the screen**, sized from the display''s
  own work area rather than a fixed 1100x760, so it is never taller or wider than
  the monitor it opens on.
- **The folder, download and cancel controls stay reachable.** They sit in a
  sticky bar at the bottom of the page, so finding them never needs scrolling at
  any window size; button labels wrap rather than being clipped, and a very long
  Reel title wraps to three lines with the full text on hover.

### Licensing and source

- **Proprietary licence.** The application is proprietary software owned by
  Mohamed Farouk Amer: redistribution, resale, sublicensing and commercial
  distribution of the developer-owned portions are not permitted without the
  developer's prior written permission, and no open-source licence is granted
  for them. Nothing in it restricts any right granted by a third-party
  component's own licence. See `LICENSE.txt`.
- **FFmpeg.** Bundled under GNU LGPL v2.1 or later, upgraded to v3 by the build.
  The complete corresponding source for the exact build, and the build system
  that produced it, are published with this release; the written offer is
  `FFMPEG-SOURCE-OFFER.md`, installed with the application.
- **Third-party notices.** `THIRD_PARTY_NOTICES.md`, installed with the
  application, covers FFmpeg, yt-dlp and its bundled components, Electron and
  Chromium, and every npm package compiled into the application.

### Known issues

- **The installer is not code-signed.** Windows SmartScreen will warn about an
  unknown publisher. The release page publishes the installer's SHA-256; verify
  it before running the file. See `SECURITY.md`.
- **Update mechanism.** Updates are mandatory by design and by licence, and the
  in-application update check ships in this version: it runs at launch, blocks
  on a confirmed newer version, and opens with a warning banner when the check
  itself cannot be answered. The updater is confined to three GitHub hosts over
  HTTPS. Because the installer is unsigned, the SHA-512 published in
  `latest.yml` is the integrity control an update checks, and a mismatch blocks
  rather than installs.
- **Facebook can break this at any time.** The application reads Facebook's
  public pages. A change on Facebook's side can stop analysis or downloading
  without notice.
- **Metadata extraction may fail before it is reached.** Live development
  testing reached the transport layer but did not confirm that a public Reel's
  metadata can always be extracted. This is untested end to end against a live
  Reel from a clean install.
- **A compromised release is the top security risk.** Because the installer is
  unsigned and runs at user privilege, the published checksums are the primary
  integrity control. See `SECURITY.md`.
- **One LGPL question is the owner's to close.** The FFmpeg build is static, and
  the source offer discharges what it can by documentation; the residual
  section 4 question for a static build needs the owner's own legal sign-off.
  See `FFMPEG-SOURCE-OFFER.md`.
  Engineering reports are maintained locally and are not included in the public
  repository.
