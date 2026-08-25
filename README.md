# Arc Comic Post Generator — Android App

This repo builds the Arc Comic Post Generator into a real Android APK using GitHub Actions.
You don't need Android Studio or a computer — GitHub's servers do the build.

## First-time setup

1. Create a new **empty** GitHub repo (e.g. `arc-post-generator-app`).
2. Upload every file in this folder to that repo, **keeping the exact folder structure**:
   ```
   your-repo/
     .github/workflows/build-apk.yml
     www/index.html
     package.json
     capacitor.config.json
   ```
3. Go to your repo's **Actions** tab. A workflow run should start automatically (or click
   "Build Android APK" → "Run workflow" to trigger it manually).
4. Wait for the run to finish (few minutes). Open the finished run, scroll to
   **Artifacts**, and download `arc-comic-post-generator-apk`.
5. Unzip it — inside is `app-debug.apk`. Transfer it to your phone and tap to install
   (you'll need to allow "install from unknown sources" once, same as any sideloaded app).

## Updating the app later

Whenever you want to change something in the app itself (not a post — the app), edit
`www/index.html` in the repo and push. Every push to `main` automatically rebuilds the APK.
Just re-download the new artifact from the latest Actions run and reinstall over the old one.

## What's inside the app

- Sidebar (☰ icon top-left) — create, switch between, and delete multiple post drafts.
  Everything autosaves as you type, so closing the app never loses your work.
- Same post builder as before: text/image/ad/button blocks, bold/italic/underline,
  GitHub image-link helper, lightbox gallery, Save/Open project files, Edit Existing Post.
- Ad codes are pre-filled with your defaults — edit them in the Ad Codes section if you
  ever need to change them.

## Notes

- This is a debug-signed APK (fine for personal installs on your own phone). If you ever
  want to publish it to the Play Store, that needs a proper release signing key — a
  separate step we can set up later if you need it.
- No internet permission is required beyond what your device's browser already needs to
  load images/ad scripts when you preview a post.
