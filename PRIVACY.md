# Snapdown Privacy Policy

<!-- Copied from the Wira Delta Indonesia legal source (snapdown/privacy.en.md) on 2026-09-26.
     Edit the source, then copy it here again. -->

This is an English translation of the Indonesian original. If the two differ in interpretation,
the Indonesian text prevails.

**In effect since:** 1 October 2026

Snapdown is software for capturing and reviewing screenshots. Everything Snapdown captures and stores lives **on your own computer only**. There is no analytics, no crash reporting, no user account, and no device identifier. This policy applies equally to all three ways Snapdown is installed: the installer from GitHub Releases, the Microsoft Store build, and the portable build made only for Scoop. Two things in the application touch the network, and the sections below describe both in full rather than summarizing them. The first, the **update check**, is on by default, sends your Snapdown version, Windows version, and computer architecture to our server at `wiradelta.com`, and can be switched off. The second, **activating Snapdown Pro**, happens only when you press Activate or Deactivate, and never on its own.

## What Snapdown Captures

Snapdown takes screenshots of your whole screen, a window, or a region, only when you trigger a capture (with a shortcut or a button). It never captures continuously or in the background. Each capture becomes a **Finding**: the image itself, plus any note, marker, or annotation you add to it.

You can also create a Finding from an image file you import, or from an image you paste from the clipboard. Snapdown reads the clipboard only when you press Paste.

When a region capture opens, Snapdown reads the position and size of the windows and panes visible on screen, so you can select an area with one click. It reads only their bounding boxes. Window titles, text, and the contents of controls are not read, and the bounding boxes are not stored.

**Be mindful of what you capture.** A screenshot can contain anything visible on your screen at that moment: passwords in a password manager left open, personal messages, account numbers, another person's information. Snapdown has no way to tell sensitive content apart from anything else on screen. That judgment is yours, both when you capture and when you copy, export, or share a bundle you built from your Findings.

## What Is Stored on Disk, and Where

| Path | Contents | Retention |
|---|---|---|
| `%APPDATA%\com.wiradelta.snapdown\library.db` | The Findings and bundles database: notes, markers, timestamps, references to the image files in the vault, and your settings | Until you delete a Finding or bundle, or delete the file yourself. The uninstaller asks whether to delete this folder too |
| `%USERPROFILE%\Pictures\SnapdownVault\` (default; the installer asks where to put it, and you can move it in Settings) | The vault: original screenshots in `findings\`, and one folder per bundle, `bundles\<id>\`, holding `bundle.md` and PNG files with the annotations burned in | Until you delete a Finding or bundle in the app, or delete the folder yourself. Snapdown does not delete original screenshots automatically, and the uninstaller never deletes the vault |
| `%APPDATA%\com.wiradelta.snapdown\vault_path.txt` and the registry key `HKCU\Software\Wira Delta Indonesia\Snapdown` (value `VaultPath`) | Where your vault is, so the installer finds it on an update or a reinstall | Until you answer Yes when the uninstaller asks about deleting data, or delete them yourself |
| `%APPDATA%\com.wiradelta.snapdown\licence.json` (only while Snapdown Pro is active) | Your license key, the activation identifier Lemon Squeezy returned, the email address the license was bought with, the activation date, and a keyed checksum | Until you press Deactivate and Lemon Squeezy confirms it (this needs an internet connection). Uninstalling with a Yes answer also deletes the file, but does not deactivate the activation |
| `%TEMP%\Snapdown-Setup-Update.exe` (only after you install an update from the app) | The downloaded update installer, already checked against its checksum | Until the next update overwrites it, or you or Windows clean the Temp folder |
| The registry key `HKCU\Software\Microsoft\Windows\CurrentVersion\Run` (value `Snapdown`) | The command that starts Snapdown when you sign in to Windows. Created the first time Snapdown runs | Until you turn off "Run Snapdown at Windows startup" in Settings. The uninstaller does not remove this value |

In the Scoop build, uninstalling through Scoop (`scoop uninstall snapdown`) removes only the application folder. The settings, database, and `licence.json` in `%APPDATA%\com.wiradelta.snapdown` stay until you delete them yourself, and the Snapdown Pro activation is not deactivated with them, so press Deactivate first.

These files and registry values live under your own Windows user account, at normal user permissions: treat them as readable by anything else running as you, the same as any other file in your user profile. Moving the vault in Settings moves every existing file to the new location; nothing is duplicated or left behind by that move.

**Deleting a Finding or a bundle is permanent.** Deleting a Finding removes its database row and its original screenshot from the vault; the burned-in copy inside any bundle that holds it stays until that bundle is deleted. Deleting a bundle removes its folder (`bundle.md` and its PNG files); its Findings stay. Files are deleted directly, not moved to the Recycle Bin, and the application has no recovery area of its own.

## Getting Your Work Out of Snapdown

There are three ways, and you start each one:

- **Copy image** copies one image to the clipboard, with or without the annotations burned in.
- **Copy Markdown** copies a bundle's Markdown to the clipboard. The text carries the full path of each image file in the vault, which usually contains your Windows user name. If you turned on the hand-off instruction in Settings, that instruction comes first in the text.
- **Export PDF** writes one PDF file to a location **you** choose in the standard Windows save dialog. In Snapdown Free, the mark in the PDF footer is a link to `https://wiradelta.com/snapdown`; opening it is an ordinary visit to our site.

After that, the result is ordinary clipboard content or an ordinary file. Snapdown has no further involvement with it, does not track where it goes, and does not upload it anywhere.

## Network Activity

Capturing, annotating, bundling, copying, and exporting are entirely offline: none of them makes a network request. **Two things in Snapdown make network requests: the update check, and activating or deactivating Snapdown Pro.** Installing an update is the only thing that downloads a file. Each is described in full below.

### The Update Check

**What is sent.** An unauthenticated HTTPS `GET` to `https://wiradelta.com/api/v1/update/snapdown/`, a server run by Wira Delta Indonesia. The request's `User-Agent` header carries four things: the product name (Snapdown), the version number of the Snapdown you run, your Windows version, and your computer's architecture (for example x64 or ARM64). Nothing else is attached: no computer name, no user name, no other hardware details, no account, no device identifier, and no counter, and only the standard headers a request cannot omit (`Host`, `Accept`). The Microsoft Store build and the Scoop build send the same check. The endpoint answers the request itself and does not redirect it to GitHub, so GitHub does not receive the update check.

**What that reveals anyway, because a request cannot hide it.** Our server sees the IP address the request came from, the time, and the contents of the `User-Agent`. The endpoint runs on the same server as the `wiradelta.com` site, behind Cloudflare. Cloudflare passes the request on to our server and also sees its IP address and contents, under Cloudflare's own privacy policy.

**What we keep, and for how long.** Our server keeps a raw record of each request (IP address, time, and `User-Agent` contents) for **30 days**, then deletes it. After that, all that remains is daily aggregate counts based on the data the app sends (app version, Windows version, architecture) and an estimated number of devices, with no IP address. We use it to know how many installations run each version, and on which Windows versions and architectures. These records are not combined with purchase data or the waitlist.

**What is not sent, and could not be.** The request carries nothing about how you use Snapdown: not how many Findings you have, not what you captured, and not whether you use Snapdown Pro.

**How to turn it off.** The automatic check every 24 hours is **on by default** on a fresh installation, and the toggle is "Check automatically every 24 hours" in Settings → About. Turning it off stops all periodic network activity; the manual "Check for Updates" button stays, so you can ask once without leaving anything running. Nothing degrades either way: the check only reports that a newer version exists, and it gates nothing.

### Installing an Update

There are three update paths. In the regular build, before installing, Snapdown shows the release notes and a link to the new version's EULA. If you choose to install an update with the Download and Install button, Snapdown downloads the installer named by the manifest from GitHub Releases in the `wiradeltaid/snapdown-releases` repository, then runs it without showing the wizard, and Snapdown reopens afterward. GitHub sees your IP address during that download, under GitHub's own privacy policy. That is the one time the application fetches something other than a small text file, and the one time it launches another program.

The manifest names a SHA-256 digest for each installer. The download is hashed while it is written and compared against that digest **before anything is executed**; a mismatch aborts and the file is never run. This step is never started by the periodic check, only by you, from Settings. In the Microsoft Store build, the version check still goes to `wiradelta.com` as above, but the install button opens the Microsoft Store: the Store installs the update, and Snapdown downloads no installer itself. In the Scoop build, the version check also goes to `wiradelta.com`, but the update button downloads no installer: it shows the command `scoop update snapdown` for you to run yourself. Scoop then downloads the new portable build and checks its SHA-256 digest against the one listed in the Scoop manifest before installing it.

### Activating Snapdown Pro

This happens **only when you press Activate or Deactivate** in Settings → About. Snapdown never contacts the licensing service on its own: not at launch, not when you export, not in the background, and not to re-check a license it has already activated.

**What is sent.** An HTTPS `POST` to Lemon Squeezy (`api.lemonsqueezy.com`), the merchant that sells Snapdown Pro on our behalf. Activating sends the license key you pasted and a label for this computer. Deactivating sends the license key and the activation identifier Lemon Squeezy returned when you activated.

**What the label is, and what it is not.** It reads like `Snapdown on Windows · 2026-09-23 · 4f1a`: the operating system, the activation date, and four random characters so you can tell your computers apart in your Lemon Squeezy order page. **It is not your computer's name**, which often contains a person's name, and it carries no hardware details.

**What that reveals anyway.** Lemon Squeezy sees the IP address the request came from, and already holds what you gave it at checkout: your name, email address, and order. Its handling of that is governed by Lemon Squeezy's own privacy policy.

**What comes back, and what we keep.** Lemon Squeezy answers whether the key is valid for Snapdown Pro, together with the email address it was bought with. Snapdown stores that answer in `licence.json` on your computer (see "What Is Stored on Disk, and Where"). We, the publisher, receive nothing from the app on this path; we see your purchase only through the merchant's order records, as any seller does.

**If you never buy Pro**, this path is never used.

## The Snapdown Pro Waitlist

The waitlist is on the `wiradelta.com` site, not in the app. The email address you sign up with is stored on our server and used to send news about Snapdown Pro and later Wira Delta Indonesia products. The basis is the consent you give when you sign up, and the signup form states this use. Every email carries an unsubscribe link; when you use it, your address is deleted from the list on our server and from the sign-up notification emails we received. The details are in the site's Privacy Policy (`wiradelta.com/privacy/`).

## Third-Party Components

Snapdown ships with Slint, IBM Plex, and Lucide icons, each under its own license; the full list of third-party components is in `NOTICE.txt` in the install folder and in the application's About tab. None of them contacts a server from inside Snapdown: they are interface and rendering libraries, and font and icon assets, not services.

## Your Rights

The only personal data from the app that reaches us is the IP address in the update check records, which is deleted after 30 days. Under Indonesia's Law No. 27 of 2022 on Personal Data Protection, you may ask to access, correct, or delete personal data about you that we hold. Snapdown Pro purchase data is held by Lemon Squeezy as the merchant; you can make a request about it to Lemon Squeezy or through us. Send requests to `support@wiradelta.com`.

## Questions

See `SECURITY.md` for how to report a security concern. For anything else about this policy, contact **support@wiradelta.com**.

## Language

This is an English translation of the Indonesian original. If the two differ in interpretation,
the Indonesian text prevails.
