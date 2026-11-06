# T−24 Receiver Field Suite 0.3

A local-first Android research instrument. This is source code, not a prebuilt APK.

## Included capabilities
- Device and OS identity summary
- User-started accelerometer, gyroscope, magnetometer and barometer sampling when available
- Configurable sampling interval and live sample preview
- Optional foreground location request, with explicit export inclusion toggle
- Cryptographically random four-direction target selection with a 1-in-5 sham condition
- SHA-256 commitment to target, condition, nonce and scheduled reveal time; in-app reveal is withheld for 24 hours
- Post-delay commitment verification and export-safe withholding of unrevealed target details
- Receiver trial log that records a response before a later target reveal
- Sensor sample export as CSV in addition to full JSON session export
- Wall-clock and monotonic elapsed-time fields
- SHA-256 hash-chained event log and local chain verification
- Export of a complete JSON session using Android's folder picker
- Classical GHZ state-vector compute benchmark at 8, 10, 12 or 14 qubits
- Research quality-control guidance and explicit limitations

## Fastest no-ProductOS build: GitHub Actions

This repository now includes `.github/workflows/android-apk.yml`. A push to `main` or a manual run builds a debug APK using GitHub-hosted Linux, Node 22 and Java 17. It installs dependencies, runs TypeScript checking, generates the Android native project, runs Gradle `assembleDebug`, and uploads `app-debug.apk` as the `t24-receiver-debug-apk` workflow artifact. No Expo login or EAS credentials are required.

Open the repository's **Actions → Android APK → latest successful run → Artifacts** and download `t24-receiver-debug-apk`. The APK is an unsigned-for-production debug install build, suitable for direct device testing. Package ID: `com.t24.receiver`.

## Alternative independent build service: Codemagic

1. Put this folder in a GitHub repository you control.
2. Create/sign in to a Codemagic account at https://codemagic.io/.
3. Connect that repository. Codemagic reads the repository to build it.
4. Select the `android-debug-apk` workflow from `codemagic.yaml` and start a build.
5. Download `app-debug.apk` from the successful build's Artifacts section.
6. Transfer it to your Android phone and install it. Android may require you to allow installs from the app used to open the APK.

The debug APK is suitable for device testing. For a public/production release, configure a private Android signing keystore in Codemagic and build a signed release APK or AAB. Never commit the keystore or passwords to the repository.

## Alternative build route: Expo EAS

```bash
npm install
npx expo-doctor
npx eas-cli login
npx eas-cli build --platform android --profile preview
```

## Local development

```bash
npm install
npm run typecheck
npx expo start
```

## Permissions and privacy
- No background location or background sensor collection.
- Motion sampling begins only after the user taps Start.
- Location is requested only after the user taps the location button.
- Storage is accessed only through Android's folder picker.
- No network upload, analytics SDK, account login, or remote collection is included.
- The app cannot grant ChatGPT or another remote process access to the phone.

## Scientific limitations
- Motion and location measurements are ordinary device sensor data, not evidence of communication through time.
- The quantum benchmark is a classical simulation, not a QPU test or quantum hardware detector.
- SHA-256 hash chaining can reveal changes to the recorded chain, but is not a hardware-backed signature and cannot prevent a privileged device owner from rewriting the entire file.
- The built-in target generator and sham selection are a local experimental aid. They do not create independent sender/receiver isolation or prove the receiver was blind.
- The 24-hour reveal gate uses the handset's local wall clock. It is a user-interface delay, not trusted time enforcement; changing the device clock or app storage can defeat it.
- The random target is stored locally by the app. A person with device-level access may inspect app storage. Do not use it as a security boundary or for high-stakes experiments.
