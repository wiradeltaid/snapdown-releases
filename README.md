# Snapdown

Turn a visual review into one Markdown file your coding agent can act on. For 64-bit Windows.

[Website](https://wiradelta.com/snapdown) | [Download](../../releases/latest) | [Changelog](CHANGELOG.md) | [EULA](EULA.md) | [Security](SECURITY.md) | [Privacy](PRIVACY.md)

---

This repository hosts the official Snapdown downloads: the installer, the portable executable, their
checksums, the update manifest, and the Scoop bucket. Snapdown is closed source, so its application
source code is not published here.

## Why

- **Describing what you can see is the slow part.** Six things wrong on a screen take longer to put
  into words than to fix.
- **Snapdown anchors every note to a place in the picture.** A numbered marker on each problem, a
  matching numbered line in the text.
- **One Markdown file to hand over.** Paste it into a coding agent conversation, or send it to a
  colleague. It reads the same way to both.
- **It stays on your computer.** No account, no sync, no telemetry. See [`PRIVACY.md`](PRIVACY.md).

## Install

**Scoop** keeps Snapdown updated alongside the rest of your Scoop apps:

```
scoop bucket add snapdown https://github.com/wiradeltaid/snapdown-releases
scoop install snapdown
```

**Direct download:** the [latest release](../../releases/latest) includes the installer
(`Snapdown-Setup.exe`) and a portable executable (`Snapdown-Portable.exe`).

**Windows SmartScreen.** The installer is not code-signed yet, so on first run Windows may show
*"Windows protected your PC"*. Choose **More info**, then **Run anyway**. To confirm the file is
genuine first, verify its checksum as described below.

## Snapdown and Snapdown Pro

Snapdown is free to use for personal and commercial work, with every feature included. Snapdown Pro
is an optional one-time licence that removes the small attribution mark from exported PDFs. Details
are at [wiradelta.com/snapdown/pro](https://wiradelta.com/snapdown/pro).

## Verify your download

Each release publishes a SHA-256 checksum for every file, in [`SHA256SUMS`](SHA256SUMS) and on the
release page. Compare it before running the file:

```powershell
Get-FileHash .\Snapdown-Setup.exe -Algorithm SHA256
```

If the values differ, do not run the file, and let us know at **support@wiradelta.com**.

## Official channels

Genuine Snapdown builds are published only through this repository's
[releases](../../releases), the Scoop bucket above, and
[wiradelta.com/snapdown](https://wiradelta.com/snapdown). Snapdown is not listed on the Microsoft
Store. An installer offered anywhere else is not from us.

## Feedback and support

- **Bugs and feature requests:** the [issue tracker](../../issues) on this repository, or
  **support@wiradelta.com**.
- **Security vulnerabilities:** report privately to **security@wiradelta.com**, not in a public
  issue. [`SECURITY.md`](SECURITY.md) explains what is in scope and what to expect.

## Licence and attribution

Copyright (c) 2026 Wira Delta Indonesia. Snapdown is proprietary software, licensed under the
[End-User License Agreement](EULA.md) that ships with every release (see also [`LICENSE`](LICENSE)).

- [`PRIVACY.md`](PRIVACY.md): what the app stores on your computer and what it sends over the network.
- [`SECURITY.md`](SECURITY.md): how to report a vulnerability and how to verify a download.
- [`NOTICE`](NOTICE): third-party dependency notices.

Snapdown ships with Slint (Slint Royalty-free Desktop, Mobile, and Web Applications license), IBM
Plex (SIL Open Font License 1.1), and Lucide icons (ISC; portions copyright Cole Bemis as part of
Feather, MIT). The same acknowledgements appear on the About tab of the application's Settings screen.
