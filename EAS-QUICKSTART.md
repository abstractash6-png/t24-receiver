# T−24 Receiver: fastest Expo EAS APK path

This project is configured for an Android APK using the `preview` EAS profile.

## 1. Put the source in GitHub
Create a new **private** GitHub repository, then upload the contents of this `t24-android` folder to the repository root (not the parent folder).

## 2. Connect Expo
Sign in at https://expo.dev with your own account. In Expo, create/open the `t24-receiver` project and connect the GitHub repository when prompted. Keep credentials and verification codes private.

## 3. Build an installable APK
If using a terminal with Node.js:
```bash
npm install
npx eas-cli login
npx eas-cli build:configure
npx eas-cli build --platform android --profile preview
```
If `build:configure` asks to initialize the project, accept the setup and let EAS add its project ID to `app.json`.

The `preview` profile is explicitly configured with `android.buildType: apk`. When the build completes, open the EAS build page on the Android phone and download/install the APK. Android may ask you to allow installs from that browser.

## Notes
- Do not send passwords, one-time codes, signing keys, or recovery phrases in chat.
- Sensor availability varies by handset. The app records measurements it can access; it does not establish retrocausality or prove information travelled backward in time.
