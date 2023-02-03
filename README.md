
# Playing video on flutter app on android using better_player is causing this error

	   Non-fatal Exception: 	io.flutter.plugins.firebase.crashlytics.FlutterError: PlatformException(error, MediaSource.Factory#setDrmSessionManagerProvider no longer handles null by instantiating a new DefaultDrmSessionManagerProvider. Explicitly construct and pass an instance in order to retain the old behavior., null, java.lang.NullPointerException: MediaSource.Factory#setDrmSessionManagerProvider no longer handles null by instantiating a new DefaultDrmSessionManagerProvider.    		Explicitly construct and pass an instance in order to retain the old behavior.

It was working previously but now it's failing due to exoPlayer. Any idea how to fix this?



Answer:

for the Android error, it tells you that you need to enable `multiDex` in your project, here is how

in `android/app/build.gradle` add this line `multiDexEnabled = true` in the `defaultConfig`

your defaultConfig should look something like this

    defaultConfig {
        // TODO: Specify your own unique Application ID (https://developer.android.com/studio/build/application-id.html).
        applicationId "com.test.test"
        minSdkVersion 21
        targetSdkVersion 30
        multiDexEnabled = true
        versionCode flutterVersionCode.toInteger()
        versionName flutterVersionName
        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
    }

regarding the iOS error it says

dependency were found, but they required a higher minimum deployment target.

so increase the minimum deployment target. you can find it in `ios/flutter/AppFrameworkInfo.plist` named `MinimumOSVersion` and looking like this

    <key>MinimumOSVersion</key> 
    <string>9.0</string>
