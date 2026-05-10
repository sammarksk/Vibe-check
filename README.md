# Cycle Companion — APK build guide

Get a real signed `.apk` in ~15 minutes. No Android Studio, no build tools.

## Files in this folder

```
index.html               The app
manifest.json            PWA manifest
service-worker.js        Offline cache + PWABuilder requirement
icon-192.png             Standard icon
icon-512.png             Standard icon
icon-maskable-512.png    Adaptive icon for Android
apple-touch-icon.png     iOS support (bonus)
```

## Step 1 — Host on GitHub Pages (5 min)

PWABuilder requires HTTPS. GitHub Pages is free and instant.

1. Go to github.com → **New repository** → name it `cycle` → public → create
2. Click **uploading an existing file** → drag in ALL files from this folder → commit
3. Repo **Settings** → **Pages** (left sidebar)
4. Source: `Deploy from a branch`, Branch: `main`, Folder: `/ (root)` → **Save**
5. Wait ~1 minute. Your URL will be: `https://YOUR_USERNAME.github.io/cycle/`
6. Open it in a browser — confirm the app loads.

## Step 2 — Build the APK with PWABuilder (5 min)

1. Go to **pwabuilder.com**
2. Paste your URL → click **Start**
3. It scores your PWA. Should be high — manifest, SW, and icons are all set.
4. Click **Package For Stores** → **Android**
5. Default settings are fine. Click **Generate Package**
6. Download the ZIP. Inside you'll find:
   - `app-release-signed.apk` ← **this is what you install**
   - `signing.keystore` ← **save this somewhere safe** (you need it for future updates)
   - `signing-key-info.txt` ← keep with the keystore

## Step 3 — Install on your phone (2 min)

1. Email/Drive/USB the `.apk` to your Android phone
2. Tap to open it
3. Android will warn "install from unknown source" → enable for your file manager
4. Install. Done.

The app icon (the burgundy crescent) appears in your launcher. Tap to open. Works offline after the first launch.

## Updating later

If you change the HTML and want a new APK:
1. Re-upload changed files to GitHub
2. Re-run PWABuilder with the **same URL** + **same package ID**
3. **Use your saved keystore** (uploaded in advanced settings) so the update installs over the existing app instead of being treated as a different app

## Troubleshooting

- **PWABuilder says manifest missing** → check `manifest.json` is at the root of your URL, not in a subfolder
- **"App not installed" on phone** → uninstall any prior version first; or you used a different keystore
- **Icon looks weird (cut off)** → that's the maskable safe zone — it's correct, Android crops it inside the launcher's chosen shape
