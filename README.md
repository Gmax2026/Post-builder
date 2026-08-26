# Arc Comic Post Generator — Android App

This turns your HTML tool into a real installable Android app using
Capacitor (a WebView wrapper), built entirely on GitHub's servers via
GitHub Actions — no PC or Android Studio needed on your end.

## One-time setup (do this once, from your phone browser or GitHub app)

1. Create a new **public or private** GitHub repo, e.g. `arc-comic-app`.
2. Upload every file in this folder to that repo, **keeping the folder
   structure exactly as-is**:
   - `.github/workflows/build-apk.yml`
   - `www/index.html`
   - `package.json`
   - `capacitor.config.json`
3. Commit directly to the `main` branch.
4. Go to the **Actions** tab of your repo. A workflow run called
   "Build Android APK" will start automatically (takes ~3-5 minutes).
5. When it finishes (green check), click into the run, scroll to
   **Artifacts**, and download `arc-comic-app-debug-apk`. That's a zip
   containing `app-debug.apk`.
6. On your phone: unzip it (any file manager can unzip), tap the
   `.apk`, allow "install from this source" if Android asks, install.

## Making changes later

Any time you edit `www/index.html` in the repo (or I send you an
updated version), just commit it to `main` — the Action rebuilds the
APK automatically. Re-download the artifact, re-install over the old
one.

## Important limitation about storage (read before testing)

This first build wraps your *current* HTML as-is. It will run as an
app, but it still uses `localStorage` internally for drafts — which,
inside a WebView APK, is more stable than a browser `file://` tab but
**still not real files**, and can still be cleared by Android under
storage pressure or an app data clear.

You said you want to test the APK build first and fix storage after —
that's the right order. When you're ready, tell me and I'll:
1. Swap the JS from `localStorage` to Capacitor's `Filesystem` +
   `@capawesome/capacitor-file-picker` plugins (already included in
   `package.json`).
2. Add a first-launch folder picker so you choose exactly where
   drafts and generated `.html`/`.json` files live.
3. Rebuild — same GitHub Actions flow, no new setup needed.

## Why not just open the HTML in a browser?

`file://` pages on Android have no reliable persistent storage and no
folder-picker access — that's the root cause of blocks vanishing and
downloads disappearing. Wrapping it as a real app is what unlocks
real file access.
