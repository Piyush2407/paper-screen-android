# Paper Screen for Android - build the APK for free via GitHub

This is the same Paper Screen project as before, now restructured as a real
Gradle project with a GitHub Actions workflow included
(`.github/workflows/build-apk.yml`). GitHub's build servers have what my own
sandbox doesn't - working internet access to Google's Android SDK servers -
so they can do the one step I couldn't: compile this into an actual
installable `.apk`. No Android Studio, no local install, nothing to trust
beyond GitHub itself.

## Step 1 - create a free GitHub account (skip if you have one)
Go to github.com and sign up. Free tier is all this needs.

## Step 2 - create a new repository
- Click the "+" top-right -> "New repository"
- Name it anything, e.g. `paper-screen-android`
- Leave it Public or Private, either works
- Do NOT check "Add a README" (you're uploading one) - click "Create repository"

## Step 3 - upload this project
On the empty repo's page, click **"uploading an existing file"**.
- Extract this zip on your computer first
- Drag the entire `PaperScreen-Android` folder's contents (not the outer
  folder itself) into the browser upload box - most browsers accept a
  folder drag-and-drop here and preserve the subfolder structure
- Scroll down, click **"Commit changes"**

If the drag-and-drop doesn't preserve folders for you, the reliable
alternative is installing **GitHub Desktop** (free, from desktop.github.com)
and using its "Add existing repository" + "Publish" buttons instead - no
command line needed either way.

## Step 4 - watch it build
- Click the **"Actions"** tab at the top of your repo
- You'll see a run called "Build Paper Screen APK" start automatically
  (triggered by your upload) - click it
- It takes 2-4 minutes. A green checkmark means it worked.

## Step 5 - download the APK
Still on that workflow run's page, scroll to the bottom to
**"Artifacts"** and click **PaperScreen-debug-apk** - this downloads a zip
containing `app-debug.apk`. That's the real, installable app.

## Step 6 - install it on your Galaxy Tab S9 FE
- Copy `app-debug.apk` onto the tablet (email it to yourself, use a cloud
  drive, or a USB cable)
- Tap the file on the tablet - Android will ask to allow installing from
  this source the first time; allow it
- Open the app, tap **"Grant 'Display over other apps'"** first (this is a
  special permission every overlay app needs - separate from the normal
  install), then tick whatever you want from the three groups: Texture,
  Light Tint, Plain White

## If the Actions build fails
Click the failed run, open the "Build debug APK" step, and the red text
will say what broke - paste it back to me and I'll fix the project. The
most likely cause would be a Gradle/Android Gradle Plugin version
mismatch, which is a one-line fix in `app/build.gradle`.

## What's in this build (unchanged from the last version)
Direct port of the Windows app: three independent, multi-tick groups -
Texture (5 paper textures), Light Tint (tube-light/LED glare, 4 warm
colors), Plain White (eyestrain, 4 gentle colors, lower opacity ceiling) -
each with its own Off button and its own intensity slider, layered through
one click-through overlay. Targets Android API 23 specifically to avoid the
stricter notification/foreground-service rules newer APIs impose, which
sidesteps a common source of overlay-app glitches on recent Android.

Simplified vs. the Windows version: no hotkeys (not available to normal
Android apps), no per-app exceptions list (would need an extra permission
grant - ask if you want it added once this base version is confirmed
working on your tablet).
