# Security Policy

## Reporting a vulnerability

**Report security issues through GitHub's private vulnerability reporting on
this repository** (the "Report a security vulnerability" link under the
Security tab). Do **not** report them by email, and do **not** open a public
issue for a security problem.

Private vulnerability reporting is preferred for a specific reason: it keeps the
report and the fix coordinated, and it keeps an unpatched defect off the public
issue tracker where anyone could exploit it before a release exists.

When you report, include:

- the version shown on the application's About information, and the installer's
  SHA-256 from the release page;
- the operating system version;
- a minimal description of what the application did, and what you expected;
- the link you used, with anything identifying removed, or a link to a Reel you
  own.

You will get an acknowledgement. This is a small project; a fix may take time,
and it will ship in a release rather than as a patch.

## The highest-severity risk: a compromised release

This application downloads and executes bundled binaries, and it installs for
the user's account without administrator rights. A build pipeline compromise —
an attacker who publishes an installer that looks like ours but is not — is
therefore the most serious risk this project faces. A malicious installer would
run with the user's own privileges, and "Windows protected your PC" is the only
system-level barrier a user sees, because the installer is not code-signed.

**How to verify a release is genuine:**

1. Take the SHA-256 of the file you downloaded:

   ```powershell
   Get-FileHash -Algorithm SHA256 "Reels-Downloader-Setup-<version>.exe"
   ```

2. Compare it with the checksum published on the release page in this
   repository. The comparison must be exact. If a single character differs, stop
   and delete the file. Every release also publishes `SHA256SUMS.txt`, which
   carries the checksums of every published file in the standard format, so the
   whole release can be checked at once (`Get-Content` in PowerShell, or
   `sha256sum -c` on Linux, macOS and WSL). See `README.md` for both.

3. Take it from this repository's Releases page, not from a mirror, a repost, a
   link in a video description, or a search result. Only the installer published
   here is supported, and the application's licence does not permit
   redistribution of it at all - so a copy that does not verify is either
   modified or not official.

   The checksum matters because a mirror that modifies the installer cannot also
   produce a hash that matches the one published here. A mirror that regenerates
   *both* the installer and its checksum file still cannot match the value quoted
   on this repository's release page and in `README.md`, which is why
   the value is published in more than one place.

4. The release page also publishes a SHA-512 the auto-updater checks
   (`latest.yml`). A checksum mismatch there stops an update from being applied:
   the application stays blocked on the old version rather than installing
   something it could not verify, and the failure surfaces as a blocked screen
   with a manual-download link rather than as a silent skip.

   This matters more than it would for an application with optional updates,
   because here updates are mandatory: a newer release is downloaded and
   installed automatically before the application opens, and the user is not
   offered a way to decline it. The integrity of a published release is
   therefore the integrity of every installation that checks for it — which is
   another reason the checksums above are the control to trust, and why a
   release is never replaced in place (see `RELEASING.md` in the source
   repository).

No member of this project will ever ask you to run a file that does not verify
against the published checksum, and none will ever send you an installer by
email or direct message.

## What this application does, and does not, do

Stated plainly, because the threat model follows from it:

- The application talks to **Facebook's public web pages** (through the bundled
  yt-dlp), to **GitHub**, once at launch, to check whether a newer release
  exists, and to **Facebook's image CDN** (`*.fbcdn.net`), once per analysed
  Reel, for that Reel's preview picture. It makes no other network connections.
  The update check is confined to a deny-by-default network policy: the
  application's update component may reach only `github.com`,
  `release-assets.githubusercontent.com`, and `objects.githubusercontent.com`,
  over HTTPS on the standard port. Every other request it attempts — another
  host, a subdomain of an allowed one, a non-HTTPS scheme, or another port — is
  cancelled before it leaves the process.

  The thumbnail fetch is confined the same way: only `*.fbcdn.net`, over HTTPS
  on the standard port, with no cookies and no credentials, no redirect that
  leaves that set, a 2 MiB cap, an eight-second deadline, and a content-type
  check backed by a magic-byte check — a response that is not actually the image
  it claims to be is discarded rather than decoded.

  Both disclose your IP address to the host concerned and nothing else. The
  thumbnail's address is never passed to the interface: the main process
  fetches, shrinks and re-encodes it and hands over a local data URL, which is
  also why the content-security policy no longer names a remote image source.
- It sends **no credentials and no cookies**. It does not accept a login and
  has no way to hold one. If a page requires an account, the download fails
  rather than prompting for a password.
- It refuses any link whose host is not on its allowlist
  (`facebook.com`, `www.facebook.com`, `m.facebook.com`, `web.facebook.com`,
  `fb.watch`) and any link shape other than the documented Reel paths.
- It connects only over HTTPS, validates certificates against the hostname it
  asked for, does not follow redirects to a different host, and does not fetch
  from or connect to anything the user did not link to.
- Settings and the last-used folder are stored locally under the user's
  profile. No telemetry is collected and nothing is uploaded.

## Out of scope

- **Content access controls are not this application's business.** If a Reel is
  not genuinely public, this tool is not the way past that, and no vulnerability
  report about "I could download a private video" will be treated as a security
  defect in this project.
- **The bundled tools are upstream projects.** A defect in yt-dlp or FFmpeg is
  theirs to fix; report it to them, and tell us so we can pin a fixed version.
- **The installer is not code-signed.** That is a known limitation, not an
  oversight; it is why the checksums above are the primary integrity control.
