# Snapdown End-User License Agreement

This is an English translation of the Indonesian original. If the two differ in interpretation,
the Indonesian text prevails.

**In effect since:** 1 October 2026

This is an agreement between you ("**you**", "**User**") and **Wira Delta Indonesia** ("**Publisher**", "**we**", "**us**"), the publisher of **Snapdown**, software for capturing and reviewing screenshots (the "**Software**"). It covers your use of the Software in its compiled binary form, from whichever channel you get it: the installer from GitHub Releases and everything it places on your computer, the Microsoft Store build, and the portable build made only for Scoop. All three are under the same license.

**By installing, copying, or otherwise using the Software, you agree to be bound by this Agreement. If you do not agree, do not install or use the Software.**

---

## 1. Snapdown and Snapdown Pro

Snapdown is provided **free of charge**, for personal and commercial use alike ("**Snapdown Free**"). PDF files exported from Snapdown Free carry a small attribution mark in the page footer.

**Snapdown Pro** is the same Software, without that mark on PDF files exported after a license key is activated. Snapdown Pro is sold as a one-time purchase through our merchant, Lemon Squeezy. No other feature differs between the two. Markdown and images you copy from Snapdown never carry the mark, in Snapdown Free or in Snapdown Pro.

The purchase itself is made with Lemon Squeezy as the merchant of record, and is also governed by its terms of sale, including invoicing and the processing of refunds. This Agreement governs your use of the Software.

Neither is open source: **no source code is distributed with the Software**. This Agreement grants you a license to *use* the compiled Software, and grants no right to the source code, the design, or the internals behind it.

## 2. License Grant

Subject to the restrictions in Section 3, the Publisher grants you a **non-exclusive, non-transferable, revocable, worldwide license** to install and run the Software, free of charge, on any number of computers you own or control, for as long as this Agreement remains in effect.

**Snapdown Pro.** If you buy Snapdown Pro, the Publisher additionally grants you a **perpetual, non-exclusive, non-transferable** license to activate it on **up to three (3) computers** you own or control at any one time. You may move an activation by deactivating it (Deactivate) on one computer and activating it (Activate) on another. Activating and deactivating need an internet connection. Uninstalling Snapdown or deleting its data folder does not deactivate the activation on that computer, so press Deactivate first. Uninstalling through Scoop removes only the application folder; the settings and `licence.json` in `%APPDATA%` stay. If a computer is lost or broken, or Snapdown was uninstalled without Deactivate, write to `support@wiradelta.com` from the email address you bought with, and we free that computer's activation slot. The license covers the Software as released, including later versions the Publisher chooses to make available under this license; it does not oblige the Publisher to release any. PDF files exported before activation are not changed by it.

## 3. Restrictions

You may **not**:

1. Reverse-engineer, decompile, or disassemble the Software, except to the extent applicable law makes this restriction unenforceable despite it being stated here.
2. Modify the Software, or create derivative works based on it.
3. Redistribute a **modified** copy of the Software, or repackage it inside another installer, bundle, or product.
4. Charge money for the Software, or place it behind a paywall, sponsorship gate, or "download manager" of your own; or sell, share, transfer, or publish a Snapdown Pro license key.
5. Remove or alter any copyright, trademark, or attribution notice contained in the Software, its installer, or its accompanying files (including third-party notices, see Section 7).
6. Use the Software in any way that violates applicable law.

You **may** mirror or redistribute the **unmodified** installer or portable build exactly as published by the Publisher (for example, on a personal blog, a software download portal, or a package-manager bucket), provided this Agreement travels with it and you do not claim authorship of the Software.

## 4. Ownership

The Software is licensed, not sold. The Publisher retains all right, title, and interest in and to the Software, including all intellectual property rights in it. This Agreement does not grant you any rights to the Publisher's trademarks or trade names.

## 5. No Warranty

**THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED**, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, AND NON-INFRINGEMENT. The Publisher does not warrant that the Software will be error-free or uninterrupted, or that it will meet your requirements.

## 6. Limitation of Liability

TO THE MAXIMUM EXTENT PERMITTED BY APPLICABLE LAW, IN NO EVENT SHALL THE PUBLISHER BE LIABLE FOR ANY INDIRECT, INCIDENTAL, SPECIAL, CONSEQUENTIAL, OR PUNITIVE DAMAGES, OR ANY LOSS OF DATA, PROFITS, OR GOODWILL, ARISING OUT OF OR IN CONNECTION WITH YOUR USE OF (OR INABILITY TO USE) THE SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGES. The Publisher's total liability arising out of this Agreement shall not exceed the amount you paid for the Software: zero for Snapdown Free, and the price you paid for your Snapdown Pro license.

Nothing in this Agreement excludes or limits liability that cannot lawfully be excluded or limited under the law that applies to you.

## 7. Third-Party Components

The Software includes third-party components under their own separate license terms, currently Slint (Slint Royalty-free license), IBM Plex (SIL Open Font License 1.1), and Lucide icons (ISC, and MIT for the Feather-derived portion). These notices appear in the application's About screen and in the files distributed alongside the Software, including `NOTICE.txt` in the install folder. Nothing in this Agreement overrides those licenses, and nothing here grants you weaker rights over those components than their own licenses do.

## 8. Your Data

The Software does not send your screenshots, notes, or bundles to the Publisher. The only thing the Publisher receives from the Software is the update check request, which reveals your IP address, the version of the Software you run, your Windows version, and your computer's architecture. The update check is on by default and can be switched off in Settings. The Privacy Policy (`PRIVACY.md`) sets out in full what the Software stores and where, what it sends over the network, and how long we keep update check records.

## 9. Updates and Support

The Publisher **may**, but is not obligated to, release updates, patches, or new versions of the Software. The Software is offered without a service-level commitment: there is no guaranteed response time and no support contract. Reports and questions are handled on a best-effort basis; see `SECURITY.md` for how to report a security issue.

Buying Snapdown Pro does not create a support contract or a guaranteed response time. If you lose your license key, write to `support@wiradelta.com` from the email address you bought with, and it will be resent.

## 10. Term and Termination

This Agreement is effective until terminated. It terminates automatically, without notice, if you fail to comply with any of its terms. Upon termination, you must stop using the Software and delete all copies of it in your possession.

If this Agreement terminates, any Snapdown Pro license you hold terminates with it. Termination for breach does not by itself entitle you to a refund. Refunds are governed by the refund policy published at `wiradelta.com/snapdown/pro/` (a full refund when requested within 14 days of purchase) and by the law that applies to you.

## 11. Governing Law

This Agreement is governed by the laws of the Republic of Indonesia, without regard to its conflict-of-law principles.

## 12. Changes to This Agreement

The Publisher may update this Agreement for a later release. The version published alongside the release you installed is the one that governs your use of that version. Before installing an update with the Download and Install button in Settings, the Software shows the release notes and a link to the Agreement that ships with that release. The update installer then runs without showing the installer's agreement page again; that Agreement is still placed in the install folder and published at `wiradelta.com/snapdown/eula/`. In the Microsoft Store build, the install button opens the Microsoft Store, and the Store installs the update. In the Scoop build, the update button shows the command `scoop update snapdown` instead of downloading an installer; Scoop installs the update and checks the portable build's SHA-256 digest from the Scoop manifest.

## 13. Contact

**support@wiradelta.com**

## 14. Language

This is an English translation of the Indonesian original. If the two differ in interpretation,
the Indonesian text prevails.

---

*Publisher: Wira Delta Indonesia. Product: Snapdown. This Agreement applies to the compiled Software only; it does not apply to and does not modify the license of any other Wira Delta Indonesia product.*
