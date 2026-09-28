# Snapdown Security Policy

<!-- Copied from the Wira Delta Indonesia legal source (snapdown/security.en.md) on 2026-09-26.
     Edit the source, then copy it here again. -->

This is an English translation of the Indonesian original. If the two differ in interpretation,
the Indonesian text prevails.

**In effect since:** 1 October 2026

Snapdown runs as a normal, **non-elevated** user process. It installs per user without Administrator rights, does not request Administrator privileges when it runs, does not install a system-wide low-level keyboard hook, and does not run a background service. Its shortcuts are registered through the standard Win32 `RegisterHotKey` API, which only delivers the key combinations you configured; that API cannot observe any other keystrokes.

Three other properties also deserve scrutiny, so we state them up front. Snapdown **registers itself to run when you sign in to Windows** on its first run (the registry key `HKCU\...\CurrentVersion\Run`, which you can switch off in Settings). When a region capture opens, Snapdown **reads the list of visible windows** (`EnumWindows`) and **walks their UI Automation tree**, only to take bounding boxes and whether each element is on screen, so you can select an area with one click; titles, text, and the contents of controls are not read. And Snapdown **downloads an installer and runs it**, only when you choose to install an update.

## Two Facts Most People Want Up Front

1. **Snapdown does not record keystrokes.** There is no call to `SetWindowsHookEx` in Snapdown's code or in the shortcut library it uses (`global-hotkey`, which uses `RegisterHotKey` on Windows). The Key check panel in Settings only reads keys pressed while Snapdown's own Settings window is focused.
2. **Snapdown makes two kinds of outbound requests, and only two.** The update check to `https://wiradelta.com/api/v1/update/snapdown/`, on our site's server behind Cloudflare, on by default every 24 hours and switchable off in Settings → About. Its `User-Agent` header carries the product name, the Snapdown version, the Windows version, and the computer's architecture, and nothing else is attached. The regular build downloads an installer from GitHub Releases if you choose to install an update; the Microsoft Store build leaves installing updates to the Microsoft Store; the Scoop build shows the command `scoop update snapdown` and leaves the download and install to Scoop. And license activation with Lemon Squeezy, only when you press Activate or Deactivate. `PRIVACY.md` sets out exactly what each request carries.

Both use the same HTTP client (`ureq`): HTTPS only, with bounded timeouts and response sizes. The license client follows no redirects at all. The update check endpoint answers itself, with no redirect to GitHub. The installer download from GitHub Releases follows at most one redirect, only to an HTTPS address, and only to a GitHub host on its allow-list. There is no analytics, no account, and **no listening socket**: nothing in the shipped build accepts an inbound connection.

## The Updater, and What Actually Verifies It

The manifest names a SHA-256 digest for each installer. The download is streamed to a temporary file, hashed as it is written, and compared against that digest **before anything is executed**; a mismatch aborts, the temporary file is deleted, and nothing is run. A redirect to a plain `http://` address is refused, so a redirect cannot quietly downgrade the transfer to unencrypted HTTP.

It is worth being exact about what that proves, because it is the same limit as the checksum guidance below: it proves the bytes that arrived are the bytes the manifest describes. It does **not** prove who wrote the manifest. That trust rests on the manifest being served over HTTPS from our official server (behind Cloudflare) and, once code signing exists, on the signature instead.

Before installing, Snapdown shows the release notes and a link to the new version's EULA. An installer that passes the check runs without showing the wizard, and Snapdown reopens. The Microsoft Store build does not use this updater: its install button opens the Microsoft Store, which installs the update. The Scoop build does not use it either: its update button shows the command `scoop update snapdown`, and Scoop checks the portable build's SHA-256 digest from the Scoop manifest before installing it. The automatic check is **on by default** on a fresh installation and can be switched off in Settings.

## Reporting a Vulnerability

Snapdown's source code is **not public**, so GitHub Security Advisories on the source repository are not reachable by an outside reporter. Please report a suspected vulnerability to:

**security@wiradelta.com**

Please do not post exploit details in a public issue or comment anywhere, including on the public release repository.

Helpful in a report: the Windows build, the Snapdown version, what you did, what happened, and, if you have one, a minimal reproduction. There is no bug bounty program, and reports are handled on a best-effort basis without a guaranteed response time.

**In scope:** anything that lets Snapdown read, write, or expose data it should not; anything that executes code you did not ask for, including anything that would let a downloaded update run without matching the manifest digest, or that would let a manifest be substituted in transit; a crash triggerable by a crafted capture, bundle, imported file, or pasted image.

**Out of scope:** an attacker who already has the same level of access to your machine that Snapdown itself runs at (a non-elevated user process cannot be a meaningful escalation target for someone who is already you on your own machine); vulnerabilities in third-party components (Slint, IBM Plex, Lucide) that are not specific to how Snapdown uses them. Report those upstream instead.

## Release Integrity

**Snapdown binaries are not code-signed yet.** Two consequences, stated plainly because both are user-visible:

- Windows SmartScreen will warn on first run ("Windows protected your PC" / unrecognized app). That is expected for an unsigned build and is not, by itself, evidence of tampering. For the same reason, that warning cannot help you tell a genuine installer from a fake one.
- Because the source is not public, **the only verification available is the published checksum**, not "build it yourself and compare." Every release publishes a SHA-256 digest per installer, in the manifest and in the `SHA256SUMS` file. The in-app updater checks it for you; if you downloaded by hand, check it yourself before running:

  ```powershell
  Get-FileHash .\Snapdown-<version>-x64-setup.exe -Algorithm SHA256
  ```

  The portable build made only for Scoop has its SHA-256 digest in the Scoop manifest, and Scoop checks it when it installs.

  A checksum published beside the file it describes proves the download was not corrupted or swapped in transit. It does **not** prove who produced the original build; that trust rests on downloading only from the official channels named in `README.md`.

Code signing is the real fix for the second point, and it is not yet in place.

## Supported Versions

Only the latest release receives fixes. There is no long-term support branch, and no service-level agreement, for Snapdown or for Snapdown Pro.

## Design Notes

- The vault (screenshots) and the library database live under your own user profile at normal user permissions (see `PRIVACY.md`). Snapdown does not elevate to protect them, and does not need to, since nothing in them requires protection from your own account.
- Deleting a Finding or bundle removes its files from disk directly, not through the Recycle Bin, and the application has no recovery area of its own, so a delete cannot be undone by reopening Snapdown.
- The uninstaller never deletes the vault. It asks whether to delete the preferences and database (`%APPDATA%\com.wiradelta.snapdown`) as well; a silent uninstall keeps them. Uninstalling through Scoop removes only the application folder; the settings, database, and `licence.json` in `%APPDATA%\com.wiradelta.snapdown` stay.
- Export PDF writes to a location you choose in the standard Windows save dialog; Snapdown does not silently write exported files anywhere else. Copy Markdown puts text on the clipboard that carries the full path of each file in the vault.
- An activated license is kept in a small file, `licence.json`, sealed with a keyed checksum (HMAC) so a casual edit is detected. That is a deterrent, not a security boundary: like every client-side license, it can be defeated by modifying the program. If the file is damaged or fails its check, Snapdown quietly runs as Free; it never treats a damaged file as an accusation.
- The application accepts a key only if Lemon Squeezy reports it as belonging to **Snapdown Pro** in the Wira Delta Indonesia store. A valid key for any other Lemon Squeezy product is refused.
- The Pro status is read once when Snapdown opens and updated when you press Activate or Deactivate. It is used in one place only: deciding whether an exported PDF carries the attribution mark.

## Language

This is an English translation of the Indonesian original. If the two differ in interpretation,
the Indonesian text prevails.
