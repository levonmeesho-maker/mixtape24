# Mixtape

A cassette-styled offline music player. This repo is set up so **GitHub builds the Android APK for you** — you don't need Android Studio or a local build environment.

## How it works

- `www/index.html` — the app itself (plain HTML/CSS/JS, runs fully offline, no server needed)
- `capacitor.config.json` — tells Capacitor to wrap `www/` into a native Android app
- `.github/workflows/build-apk.yml` — a GitHub Actions workflow that installs Capacitor, generates the Android project, and builds a debug `.apk` automatically

## Steps to get your APK

1. **Create a new GitHub repository** (public or private, doesn't matter).
2. **Upload every file in this folder** to the repo, keeping the same structure:
   ```
   your-repo/
     .github/workflows/build-apk.yml
     www/index.html
     package.json
     capacitor.config.json
     .gitignore
     README.md
   ```
   Easiest way: on GitHub, click **Add file → Upload files**, drag the whole folder in, and commit directly to `main`.
3. Go to the **Actions** tab of your repo. A workflow run called **Build Android APK** should start automatically (it triggers on every push to `main`). If it doesn't, click **Run workflow** manually.
4. Wait for the run to finish (a few minutes — it's installing the Android SDK and compiling).
5. Once it's green, open the finished run and scroll down to **Artifacts**. Download **mixtape-debug-apk** — it's a zip containing `app-debug.apk`.
6. Transfer `app-debug.apk` to your Android phone (email it to yourself, use a cloud drive, or a USB cable) and tap it to install. Android will ask you to allow installs from this source the first time — that's expected for an app not from the Play Store.

## Notes

- This produces a **debug** APK, which is unsigned/self-signed and fine for installing on your own device, but not for publishing to the Play Store. If you eventually want a Play Store release, that requires generating a signing key and building a release APK/AAB — a different process.
- The app stores nothing on a server — songs you add live only in the app's memory on your device for that session, same as the browser version.
- To change the app name or icon later, edit `capacitor.config.json` (`appName`) and re-run the workflow; icons can be added under `android/app/src/main/res/` once the Android project exists, or via `npx cap` icon tooling.
