FORMA - ANDROID APP (APK) BUILT BY GITHUB, FREE
================================================

What this is
------------
A small Android app that opens your Forma web app (https://forma1234565.netlify.app/)
full screen, like a normal app, with the Forma icon. Google sign-in works because the
page runs inside Chrome. Your data and Google Drive backup are the same as the web app.
It needs internet the first time; after that Forma's own offline cache works too.

Because it shows your hosted site, a new Forma version = deploy to Netlify, and the app
updates itself. You only rebuild this APK if you change the icon, name or address.

BEFORE YOU INSTALL: deploy the latest forma-web.zip to Netlify first
--------------------------------------------------------------------
It contains assetlinks.json, the file that lets Android hide the browser address bar.
Check it opens:  https://forma1234565.netlify.app/.well-known/assetlinks.json
(you should see text starting with  [ { "relation" ... )

STEP 1 - Put this folder on GitHub (PowerShell, inside this folder)
-------------------------------------------------------------------
1. On github.com click + > New repository. Name it  Forma-apk . Leave "Add a README" OFF.
   Click Create repository.
2. In PowerShell:

   cd "C:\path\to\FormaAPK"
   git init
   git add .
   git commit -m "Forma APK"
   git branch -M main
   git remote add origin https://github.com/YOUR-GITHUB-NAME/Forma-apk.git
   git push -u origin main

   If the commit says "Please tell me who you are", run these two lines, then redo
   the commit and push:
   git config --global user.name "Yadin"
   git config --global user.email "your-github-email@example.com"

   If it says "remote origin already exists":
   git remote set-url origin https://github.com/YOUR-GITHUB-NAME/Forma-apk.git

STEP 2 - Let GitHub build it (about 3-5 minutes)
------------------------------------------------
1. Open the repo > Actions tab. If GitHub asks, click the green button to enable workflows.
2. Click "Build APK". A yellow dot = building, green check = done, red X = failed.
3. Click the finished run, scroll to Artifacts, click Forma-apk. It downloads as a zip.
4. Unzip it. Inside is Forma.apk.

STEP 3 - Install on the phone
-----------------------------
1. Send Forma.apk to the phone (USB cable, Google Drive, or email it to yourself).
2. Tap it. Allow "install unknown apps" if asked. If Play Protect warns, tap Install anyway.
3. Open Forma from your app list.

If it shows a thin address bar at the top
-----------------------------------------
That means Android could not verify assetlinks.json yet. Check:
- the link in "BEFORE YOU INSTALL" opens and shows the JSON,
- then uninstall the app, reinstall Forma.apk, and open it while online.
The app still works with the bar; it just doesn't look 100% like an app.

If the build fails (red X)
--------------------------
Click the failed run > click the red step > copy the last ~30 lines of error text and
send them to me. I could not run the Android build myself, so the first run is the test.

What's inside (so you can change things later)
----------------------------------------------
- app/src/main/AndroidManifest.xml  : the web address (DEFAULT_URL) and colours
- app/src/main/res/                 : the icons and the app name
- signing/forma-debug.keystore      : the key the APK is signed with (password: android).
  Keep using the same one so updates install over the old app. It is not a secret key,
  so make the repo Private if you don't want others to be able to sign apps as "you".
- Package name: app.forma.tracker
