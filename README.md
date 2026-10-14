# Remote Control for Android

Public, signed binary distribution. Application source is kept separately.

Install [launcher 1.132](launcher/RemoteClient-launcher-1.132.apk) once, without
uninstalling an existing client. Launchers 1.129/1.130 also support the current
runtime and notification dot. Launcher 1.131 additionally checks on client
readiness/resume (including restored tasks), when Internet access is available;
install this APK over the existing app to get that launcher-side improvement.
On first launch it downloads the signed
runtime from `release/`. Subsequent launches use the verified local copy and
check for updates in the background. **Settings → Check for updates** shows the
installed/available version and lets you install an update. Applying it requires
a restart; active remote sessions are never hot-swapped.

`release/update.json` contains a base64-encoded metadata payload and an ECDSA
P-256/SHA-256 signature. The launcher pins the corresponding public key and
verifies the signature, ZIP hash, and every file before executing any code.
The runtime ZIP contains only a DEX/resources container (`client.apk`, not a
second installed app) and ABI-specific native libraries. It contains no user
settings, pairing credentials, source code, or private signing keys.

Existing settings are preserved when upgrading the old full client APK to the
launcher with the same Android signing identity. Do not uninstall the app first.
Android 11 (API 30) or newer is required. The first download requires Internet;
a verified cached client works offline.

New Android permissions/components, trust-pin changes, and launcher fixes still
require a new launcher APK. Dynamic executable-code distribution is intended
for GitHub/sideloading, not Google Play.

Developer support: Discord `ergent95`.

Runtime 1.131 adds a red notification dot to Settings when a verified update
is available and a live update status in General settings. Pairing invitations
explicitly select Local or Relay storage regardless of the current connection
mode; scanning confirms which invitation was saved.

Runtime 1.132 fixes the QR scanner crash caused by colliding launcher/runtime
resource IDs. The runtime now uses a separate resource package (`0x80`), while
the installed launcher's resources keep `0x7f`. Install the client update from
Settings and restart; this scanner fix also works with launcher 1.129/1.130 and
does not require another APK installation or removal of existing settings.

Runtime 1.130 added portable configuration export/import in General settings.
Passwords, pairing QR codes, certificates and PC addresses are excluded. Missing
fields in old configuration codes preserve current preferences; PC profiles are
mapped by ordinal position rather than the sender's identity.
