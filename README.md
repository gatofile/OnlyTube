# OnlyTube

Mobile YouTube browser for Android 8.0+, with uBlock Origin, persistent login, background audio and silent lock-screen media controls. Independent app, not affiliated with the original service or OnlyFans.

Current version: **1.6.1**. See [app details](README.txt) and [license notices](THIRD_PARTY_NOTICES.txt).

## Build

Install JDK 17+ and Android SDK 37 / Build Tools 36.0.0, set `ANDROID_HOME`, then run:

```sh
python3 scripts/prepare-assets.py
chmod +x gradlew
./gradlew :app:assembleDebug
```

The checksum-verified `vendor/extensions.zip` contains the exact bundled extensions. It is restored locally before building, keeping upstream files unchanged. Upstream source archives and font licenses are included.

Release signing uses the existing private key supplied externally via `TUBEONLY_KEYSTORE` and `TUBEONLY_KEY_PASSWORD` (alias `tubeonly`). Signing secrets are never committed.

## Releases and update checks

The app checks the latest published release's `update.json` when opened and asks before downloading a newer APK. Draft releases are invisible to this check.

The release workflow prepares a draft with source and update metadata. Upload the matching signed **OnlyTube-1.6.1.apk** to that draft, then re-run the workflow job. It verifies the APK against the recorded SHA-256 before publishing.

For future versions, increment `versionCode` and `versionName`, build with the same signing key, run `python3 scripts/prepare-release.py`, and commit the matching `release-info/update.json`.
