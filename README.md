# Remote Control for Android

Public, signed binary distribution. Application source is kept separately.

Install the APK in `launcher/` once. On first launch it downloads the signed
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
