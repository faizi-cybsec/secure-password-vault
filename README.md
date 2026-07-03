# Building Vault as an Android APK

This folder wraps your `vault.html` app in a native Android shell using Capacitor,
so it installs and runs like any other app — no browser needed, still 100% offline.

You'll need a computer (Windows/Mac/Linux) — this build step can't happen on your phone.

## One-time setup (about 30-45 min)

1. **Install Node.js** — download from https://nodejs.org (choose the LTS version). This lets you run the build tools.
2. **Install Android Studio** — download from https://developer.android.com/studio.
   During setup, let it install the Android SDK (default options are fine).
3. Open a terminal (Command Prompt / Terminal app) and check both installed correctly:
   ```
   node -v
   ```
   You should see a version number.

## Build steps

1. Unzip this project folder somewhere, e.g. `Documents/vault-app`.
2. Open a terminal **inside that folder** (on Windows: open the folder, type `cmd` in the address bar and hit Enter; on Mac: right-click the folder → "New Terminal at Folder" if you have that option, or `cd` into it manually).
3. Install dependencies:
   ```
   npm install
   ```
4. Add the Android platform:
   ```
   npx cap add android
   ```
5. Copy your web app into the Android project:
   ```
   npx cap sync android
   ```
6. Open the project in Android Studio:
   ```
   npx cap open android
   ```
   This launches Android Studio with your app loaded. First launch may take a few minutes while it downloads Gradle/SDK components — let it finish.
7. In Android Studio, go to **Build → Build Bundle(s) / APK(s) → Build APK(s)**.
8. When it finishes, click the "locate" link in the notification (or find it at `android/app/build/outputs/apk/debug/app-debug.apk`).

## Getting it onto your phone

- Plug your phone in via USB, enable "USB debugging" in Developer Options, and in Android Studio click the green Run ▶ button — it installs straight to your phone.
- Or just copy `app-debug.apk` to your phone (email it to yourself, USB transfer, etc.), open it with a file manager, and tap Install. You'll need to allow "install from unknown sources" the first time — that's normal for anything not from the Play Store.

## Updating the app later

If you change `www/index.html` (your vault code), just re-run:
```
npx cap sync android
```
then rebuild the APK in Android Studio (step 7).

## Why this approach

Capacitor doesn't rewrite your app — it just puts your existing HTML/CSS/JS inside a
native Android WebView with no browser UI around it. Your encryption, storage, and all
your vault logic work exactly the same as the version you tested in Chrome.
