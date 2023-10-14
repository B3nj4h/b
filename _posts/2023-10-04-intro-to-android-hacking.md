---
layout: post
title: Getting started with android hacking
date: '2023-10-04 20:52:04 +0800'
image: /assets/img/cover_images/1.png
categories: [Android hacking, Intro to android hacking]
tags: [Android]
---

## Getting started with android hacking

Android is a mobile based operating system based on a modified version of the linux kernel. Android was developed by the Open handset Alliance and later acquired by Google. At its core, the operating system is known as Android Open Source Project (AOSP)

## Android package
an apk file is a archive file that contains the files needed by the application to run. it can be unpacked by the following command

```bash
unzip app_name.apk
```

```bash
AndroidManifest.xml
classes.dex
kotlin
META-INF
res
resources.arsc
```

* AndroidManifest.xml: A manifest file that describes the application's package name, activities, resources, version, etc.

* classes.dex:  Contains all the java classes in a dex (Dalvik Executable) file format, to be executed by the Android Runtime.

* lib: Contains native libraries with compiled code, for different device architectures.

* META-INF: Contains verification information that is generated when the app is signed.

* res: Contains predefined application resources, like XML files that define a state list of colors, user interface layout, fonts, values, etc. 

* resources.arsc: Contains precompiled resources. It holds information that will link the code to resources.

* Assets: Contains assets that developers bundle with the application, and can be retrieved by the AssetManager. These assets can be images, videos, documents, databases, etc.

## Tools for android pentesting

There are alot of tools for android pentesting but these are the most common ones which you'll mostly need and use.

* [Android Studio](https://developer.android.com/studio): A software used to develop android apps. To understand android applications you need to develop some applications.

* [Genymotion](https://www.genymotion.com/): You can use any android virtual device of your choice but genymotion is a good choice for a vitual rooted device.

* [Android SDK platform tools](https://developer.android.com/tools/releases/platform-tools): Android SDK Platform-Tools is a component for the Android SDK. It includes tools that interface with the Android platform, primarily adb and fastboot

* [JADX](https://github.com/skylot/jadx.git): Dex to Java decompiler, Command line and GUI tools for producing Java source code from Android Dex and Apk files

* [APKTOOL](https://apktool.org/): A tool for reverse engineering Android apk files

* [Burp Suite](https://portswigger.net/burp): A set of tools used for web applications penetration testing.

* [Frida](https://frida.re/): Dynamic instrumentation toolkit for developers, reverse-engineers, and security researchers.

* [Ghidra](https://ghidra-sre.org/): A software reverse engineering (SRE) suite of tools developed by NSA's Research Directorate in support of the Cybersecurity mission

* [Drozer](https://labs.withsecure.com/tools/drozer): Comprehensive security and attack framework for Android.

* [MobSF](https://github.com/MobSF/Mobile-Security-Framework-MobSF.git): Mobile Security Framework (MobSF) is an automated, all-in-one mobile application (Android/iOS/Windows) pen-testing, malware analysis and security assessment framework capable of performing static and dynamic analysis.

