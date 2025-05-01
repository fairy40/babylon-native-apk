AetheriumApp/
├── CMakeLists.txtcmake_minimum_required(VERSION 3.10)
project(AetheriumApp)

set(CMAKE_CXX_STANDARD 17)

add_library(native-lib SHARED
    src/main.cpp
    src/BabylonApp/App.cpp
)

include_directories(include)

find_library(log-lib log)

target_link_libraries(native-lib
    ${log-lib}
)

├── AndroidManifest.xml<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.aetheriumapp">
    <application android:label="AetheriumApp">
        <activity android:name=".MainActivity"
            android:exported="true"
            android:theme="@android:style/Theme.NoTitleBar.Fullscreen">
            <intent-filter>
                <action android:name="android.intent.action.MAIN"/>
                <category android:name="android.intent.category.LAUNCHER"/>
            </intent-filter>
        </activity>
    </application>
</manifest>

├── build.gradleapply plugin: 'com.android.application'

android {
    compileSdkVersion 31
    defaultConfig {
        applicationId "com.example.aetheriumapp"
        minSdkVersion 24
        targetSdkVersion 31
        ndk {
            abiFilters "armeabi-v7a", "arm64-v8a"
        }
    }
    externalNativeBuild {
        cmake {
            path "CMakeLists.txt"
        }
    }
}

dependencies {}

├── src/
│   ├── main.cpp#include <jni.h>
#include "App.h"

extern "C"
JNIEXPORT void JNICALL
Java_com_example_aetheriumapp_MainActivity_nativeInit(JNIEnv *env, jobject /* this */) {
    InitApp();
}

│   └── BabylonApp/#include "App.h"
#include <android/log.h>

void InitApp() {
    __android_log_print(ANDROID_LOG_INFO, "AetheriumApp", "App initialized successfully.");
    // Aqui você integrará Babylon.js Native (adicionaremos em breve)
}

│       └── App.cpp
└── include/
    └── App.h#pragma once

void InitApp();



