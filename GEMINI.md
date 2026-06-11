# BlackScreen

BlackScreen is an ultra-lightweight Android application designed to display a full-screen black overlay. It is intended for use in scenarios where you want to dim the screen completely while keeping the device awake.

## Features

- **Full-Screen Black Overlay:** Hides all system UI (status bar, navigation bar).
- **Keep Screen On:** Prevents the device from sleeping while the app is active.
- **Double-Tap to Exit:** Simple gesture to close the app and return to the system.
- **Auto-Exit on Sleep:** Automatically kills itself when the power button is pressed to avoid confusion.
- **Persistent Notification:** Uses a Foreground Service to prevent the system from reclaiming resources.
- **Ultra-Lightweight:** Optimized for size (< 1MB expected after R8).

## Architecture

- **`MainActivity`**: The main UI component. Handles immersive mode, gesture detection, and permission requests.
- **`BlackScreenService`**: A Foreground Service that maintains a persistent notification to ensure the app stays alive in the background.
- **`ACTION_SCREEN_OFF` Receiver**: A BroadcastReceiver inside `MainActivity` that terminates the app when the screen turns off.

## Building and Running

The project uses Gradle. To build a **Debug APK** (recommended for testing as it is automatically signed):

```bash
./gradlew assembleDebug
```

The APK will be located at `app/build/outputs/apk/debug/app-debug.apk`.

To build a **Release APK**:

```bash
./gradlew assembleRelease
```

The APK will be located at `app/build/outputs/apk/release/app-release-unsigned.apk`. **Note:** Release builds must be signed manually before they can be installed on a device.

## Optimization

The app avoids heavy libraries like `AppCompat` or `Material Components`. It uses standard Android `Activity` and `Service` classes to minimize the DEX size. R8 minification and resource shrinking are enabled for release builds.

## CI/CD

GitHub Actions are configured in `.github/workflows/build.yml` to automatically build the release APK on every push to the `main` branch.
