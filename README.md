# YutoBok Android

A small Android WebView app for the two websites:

- **YutoBok:** https://yutobok.netlify.app/
- **Muzikasa:** https://muzikasa.netlify.app/

## Features

- Two pinned home tabs. The home tabs never display a close (`×`) control.
- Pop-ups created by a user tap and cross-site links tapped from a pinned home tab open in disposable tabs.
- Every temporary tab has an `×` close control. Pressing the phone's Back button while a temporary tab is selected closes that tab and returns to the last home tab.
- The two main WebViews are kept separate; opening a temporary tab does not replace the current home page.
- Temporary tabs are capped at four to reduce memory pressure. Automatic pop-ups without a user gesture are blocked.
- Uses the supplied pineapple picture as the app icon and the small logo at the top-left inside the app.
- Includes HTML file-picker support, direct-file downloads, fullscreen web video support, persistent cookies, and a renderer-crash recovery path.

This is a web wrapper, not an offline copy of the sites. Internet access is required. Websites and third-party advertising networks can behave differently depending on how their links and pop-ups are implemented; no wrapper can guarantee that every advertisement opens a new tab.

## Build an APK on GitHub (recommended)

1. Download and extract this project ZIP.
2. Create a new repository on GitHub.
3. Upload **all files inside** the extracted `YutoBokAndroid` folder to the repository root. The `.github/workflows/build-apk.yml` file must be included.
4. Open the repository's **Actions** tab and select **Build YutoBok APK**. If the workflow has not started automatically after the upload, press **Run workflow**.
5. Wait for the run to finish successfully. Open that run and download the **YutoBok-APK** artifact.
6. Extract the artifact ZIP to get `app-debug.apk`, then transfer the APK to your Android phone and install it. Android may ask you to allow installation from that file manager/browser.

The workflow builds with Java 17, Android SDK API 37, Android Gradle Plugin 9.3.0, and Gradle 9.5.0. The APK is a debug build suitable for testing and sideloading; it is not a signed release for Play Store publishing.

## App behavior and limits

- Main tab 1 is always **YutoBok**; main tab 2 is always **Muzikasa**.
- Up to four additional tabs can exist at once. Close one before opening more if the limit is reached.
- A same-tab link that navigates from a main site to another host is moved to a temporary tab when it comes from a user tap. WebView pop-ups created without a user gesture are intentionally blocked for security.
- When a temporary tab is active, device Back closes it immediately. When a main tab is active, Back follows that web page's history first; if there is no history, Back returns from Muzikasa to YutoBok or exits from YutoBok.
- Performance and video playback depend on the phone's Android System WebView/Chrome component and the websites themselves. Test the APK on your own phone before relying on it.
