---
layout: post
title:  "How to install ABD command in Terminal MacOSX"
author: testing4everyone
categories: [ jmeter, tutorial ]
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

## Some basic commands with ADB command
1. `adb devices`: Check if your device is connected and recognized.
2. `adb install <path/to/apk>`: Install an APK file. You should input the package name of application that you want to install.
3. `adb uninstall <package_name>`: Uninstall an app. You should input the package name of application that you want to uninstall.
4. `adb shell`: Access the device's shell to execute commands. 
5. `adb push <local_file> <remote_path>`: Copy a file from your computer to the device.
6. `adb pull <remote_file> <local_path>`: Copy a file from the device to your computer. 
7. `adb reboot`: Restart the device.
8. `adb reboot recovery`: Boot into recovery mode