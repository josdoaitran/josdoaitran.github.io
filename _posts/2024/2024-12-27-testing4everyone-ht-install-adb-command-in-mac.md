---
layout: post
title:  "How to install ABD command in Terminal MacOSX"
author: testing4everyone
categories: [ terminal, tutorial ]
image: assets/images/general-sharing/how-to-image.png
---

# Overview
In this post, I would like to collect the essential steps to help you install and setup ADB command in terminal of MacOSX. 
Firstly, we answer this question together: "What is ADB command ?"

# What is ADB command ?
- ADB stands for `Android Debug Bridge`. In terminal or command line, it is a command for us communicate the android devices.
- As a crucial tools for a software engineer, quality engineer, ...

## Install ADB command steps
In prerequisite, you have to install `brew` command in your local.
- Install brew:
Run this command in your terminal
```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```                                 
- Install Android Platform-tools using Homebrew
To install ADB command, we need to install `Android Platform-Tools` via `HomeBrew`
```shell
brew install --cask android-platform-tools
```
![walking]({{ site.baseurl }}/assets/images/setup-macosx/install-android-platform-tool.png)
You can check whether your device was installed and set up ADB command successfully or not by this command.
```shell
adb device
```
Response might be: (Due to I opened an Emulator in my Macbook)
```shell
adb devices
List of devices attached
emulator-5554	device
```
- Install Android Debug Bridge from Android Studio
You need to do these steps:
+ Download and Install Android Studio.
+ Open Android Studio -> SDK Manager -> Android SDK -> SDK Tools -> Check on Android SDK Platform-Tools -> Apply

Step 1: Open SDK manager from Android Studio
![walking]({{ site.baseurl }}/assets/images/android-studio/open-sdk-manager.png)
Step 2: On SDK tools tab, check on Android SDK Platform Tools to install
![walking]({{ site.baseurl }}/assets/images/android-studio/install-adm-android-sdk-platform-tools.png)

## Some basic commands with ADB command
1. `adb devices`: Check if your device is connected and recognized.
```shell
adb devices
List of devices attached
emulator-5554	device
```
2. `adb install <path/to/apk>`: Install an APK file. You should input the package name of application that you want to install.

`adb uninstall <package_name>`: Uninstall an app. You should input the package name of application that you want to uninstall.

4. `adb shell`: If only 1 device, to access the device's shell to execute commands.
or Using `adb shell -s device_id` if there are more than 1 device connected to your computer.
Example:
```shell
$ adb devices
List of devices attached 
emulator-5554   device
7f1c864e    device
adb -s 7f1c864e shell
```
5. `adb push <local_file> <remote_path>`: Copy a file from your computer to the device.

6. `adb pull <remote_file> <local_path>`: Copy a file from the device to your computer. 
7. `adb reboot`: Restart the device.
8. `adb reboot recovery`: Boot into recovery mode