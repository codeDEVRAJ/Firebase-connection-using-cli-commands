# 🔥 Complete Firebase + Flutter Setup Guide (2025)

This document contains every step needed to fully connect Firebase to a Flutter project.

---

## ✅ 1. Install Firebase CLI

```
npm install -g firebase-tools
firebase login
```

---

## ✅ 2. Install FlutterFire CLI

```
dart pub global activate flutterfire_cli
```

### If command not found (PATH issue)

```
$env:Path += ";C:\Users\<your_name>\AppData\Local\Pub\Cache\bin"
```

Replace `<your_name>` with your actual username.

---

## ✅ 3. Add Firebase core package

```
flutter pub add firebase_core
flutter pub get
```

---

## ✅ 4. Configure Firebase in the project

```
flutterfire configure
```

This creates:

* `firebase_options.dart`
* connects your Android/iOS app to Firebase
* adds `google-services.json`

---

## ✅ 5. Update Android build files

### **android/build.gradle.kts**

Add inside `buildscript {}`:

```kotlin
buildscript {
    dependencies {
        classpath("com.google.gms:google-services:4.4.0")
    }
}
```

### **android/app/build.gradle.kts**

Ensure plugin exists:

```kotlin
plugins {
    id("com.google.gms.google-services")
}
```

`google-services.json` must be in:

```
android/app/google-services.json
```

---

## ✅ 6. Update main.dart

Replace your main() with:

```dart
Future<void> main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp(
    options: DefaultFirebaseOptions.currentPlatform,
  );
  runApp(const MyApp());
}
```

---

## ✅ 7. Clean and rebuild project

```
flutter clean
flutter pub get
flutter run
```

---

## ✅ 8. Get SHA Keys

```
cd android
./gradlew signingReport
```

Copy:

* SHA-1
* SHA-256

Add both to Firebase → Project Settings → Android App.

---

## ✅ 9. Restart app after adding SHA

```
flutter clean
flutter pub get
flutter run
```

---

## 🎉 Firebase Setup Complete

Your Flutter app is now fully connected to Firebase and ready for:

* Auth
* Firestore
* Storage
* Messaging
* Analytics
* Remote Config
* Functions
