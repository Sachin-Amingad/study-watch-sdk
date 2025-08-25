# Flutter Environment Setup for Study Watch SDK

This guide describes how to set up a basic Flutter project that integrates the Study Watch SDK.

## 1. Install Flutter

1. Download the Flutter SDK from the [official site](https://docs.flutter.dev/get-started/install).
2. Extract the archive and add the `flutter/bin` directory to your `PATH`.
3. Verify the installation:

```bash
flutter --version
```

## 2. Create a New Flutter Project

```bash
flutter create study_watch_example
cd study_watch_example
```

## 3. Add Android Study Watch Dependency

Edit `android/app/build.gradle` and add the Study Watch SDK:

```gradle
dependencies {
    implementation 'com.github.analogdevicesinc:study_watch_sdk:4.2.1'
}
```

Also ensure that `mavenCentral()` is present in the repository list in `android/build.gradle`:

```gradle
allprojects {
    repositories {
        google()
        mavenCentral()
    }
}
```

## 4. Communicate with the Native SDK

Create a Flutter `MethodChannel` to communicate with the Android Study Watch SDK. Example:

```dart
import 'package:flutter/services.dart';

class StudyWatch {
  static const _channel = MethodChannel('study_watch');

  static Future<String?> get firmwareVersion async {
    final version = await _channel.invokeMethod<String>('getFirmwareVersion');
    return version;
  }
}
```

Implement the corresponding method in `android/src/main/kotlin/.../StudyWatchPlugin.kt` to call into the Study Watch SDK.

## 5. Run the App

Connect an Android device or emulator and run:

```bash
flutter run
```

The Flutter app can now access Study Watch features through the native plugin layer.

