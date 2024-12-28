---
layout: post
title:  "Less than 5 minutes to root an Android Device"
author: testing4everyone
categories: [ android-studio, tutorial ]
image: assets/images/general-sharing/how-to-image.png
---

# What is Root or Root Access to an Android device
Root access on an Android device is similar to administrator access on a computer (Access as Root user in an Android device). It gives you complete control over your device's operating system, allowing you to:
- modify system files
- install custom software.
- perform actions that are otherwise restricted by the manufacturer.

Default, the EndUser doesn't have the access permission as Root user in an Android devices. 
For instances, I use ADB command to access to devices and try to switch to Root user, but I can NOT do that step.

If you don't know ADB command, you can refer to these documents:
- ADB command from Android developer: https://developer.android.com/tools/adb
- ADB command in my blog: https://josdoaitran.github.io/testing4everyone-ht-install-adb-command-in-mac/

# Why we need to have a rooted Android device in testing ?
In certain cases, testing is necessary to ensure your application prevents installation and execution on compromised devices.
Rooted devices, which often have altered default configurations, are considered insecure.
Utilizing a rooted device can facilitate testing in this specific test scenario.
# How to check a device is rooted or not ?
Root check app in Android device
Link: https://play.google.com/store/apps/details?id=com.jrummyapps.rootchecker&hl=en
Or Searching: Root app in Google Store.
![walking]({{ site.baseurl }}/assets/images/android-studio/android-device-check-root.png)
Root checker in Home screen
![walking]({{ site.baseurl }}/assets/images/android-studio/android-device-check-root-home-screen.png)
![walking]({{ site.baseurl }}/assets/images/android-studio/android-device-not-rooted.png)
# How to root an Android device ?
We use RootAVD to root an Android device: https://gitlab.com/newbit/rootAVD
## Step 1 - Clone AVD into your computer
Run this command in your computer to clone source code of RootAVD (Precondition, you need to install Git in your computer)
```shell
git clone https://gitlab.com/newbit/rootAVD.git
```
Result:
```shell
Cloning into 'rootAVD'...
remote: Enumerating objects: 563, done.
remote: Counting objects: 100% (50/50), done.
remote: Compressing objects: 100% (38/38), done.
remote: Total 563 (delta 31), reused 21 (delta 12), pack-reused 513 (from 1)
Receiving objects: 100% (563/563), 72.46 MiB | 23.04 MiB/s, done.
Resolving deltas: 100% (343/343), done.
```
## Run ADV script
- Open rootAVD folder, and run rootAVD script.
![walking]({{ site.baseurl }}/assets/images/android-studio/root-avd-folder.png)
- Run rootAvd script to listAllAVDs
```shell
sh rootAVD.sh ListAllAVDs
```

We will receive the list of available AVD, such as:
```
./rootAVD.sh ListAllAVDs
./rootAVD.sh InstallApps

./rootAVD.sh system-images/android-Baklava/google_apis_playstore/arm64-v8a/ramdisk.img
./rootAVD.sh system-images/android-Baklava/google_apis_playstore/arm64-v8a/ramdisk.img FAKEBOOTIMG
./rootAVD.sh system-images/android-Baklava/google_apis_playstore/arm64-v8a/ramdisk.img DEBUG PATCHFSTAB GetUSBHPmodZ
./rootAVD.sh system-images/android-Baklava/google_apis_playstore/arm64-v8a/ramdisk.img restore
./rootAVD.sh system-images/android-Baklava/google_apis_playstore/arm64-v8a/ramdisk.img InstallKernelModules
./rootAVD.sh system-images/android-Baklava/google_apis_playstore/arm64-v8a/ramdisk.img InstallPrebuiltKernelModules
./rootAVD.sh system-images/android-Baklava/google_apis_playstore/arm64-v8a/ramdisk.img InstallPrebuiltKernelModules GetUSBHPmodZ PATCHFSTAB DEBUG
./rootAVD.sh system-images/android-Baklava/google_apis_playstore/arm64-v8a/ramdisk.img AddRCscripts

./rootAVD.sh system-images/android-34/google_apis/arm64-v8a/ramdisk.img
./rootAVD.sh system-images/android-34/google_apis/arm64-v8a/ramdisk.img FAKEBOOTIMG
./rootAVD.sh system-images/android-34/google_apis/arm64-v8a/ramdisk.img DEBUG PATCHFSTAB GetUSBHPmodZ
./rootAVD.sh system-images/android-34/google_apis/arm64-v8a/ramdisk.img restore
./rootAVD.sh system-images/android-34/google_apis/arm64-v8a/ramdisk.img InstallKernelModules
./rootAVD.sh system-images/android-34/google_apis/arm64-v8a/ramdisk.img InstallPrebuiltKernelModules
./rootAVD.sh system-images/android-34/google_apis/arm64-v8a/ramdisk.img InstallPrebuiltKernelModules GetUSBHPmodZ PATCHFSTAB DEBUG
./rootAVD.sh system-images/android-34/google_apis/arm64-v8a/ramdisk.img AddRCscripts

./rootAVD.sh system-images/android-34/google_apis_playstore/arm64-v8a/ramdisk.img
./rootAVD.sh system-images/android-34/google_apis_playstore/arm64-v8a/ramdisk.img FAKEBOOTIMG
./rootAVD.sh system-images/android-34/google_apis_playstore/arm64-v8a/ramdisk.img DEBUG PATCHFSTAB GetUSBHPmodZ
./rootAVD.sh system-images/android-34/google_apis_playstore/arm64-v8a/ramdisk.img restore
./rootAVD.sh system-images/android-34/google_apis_playstore/arm64-v8a/ramdisk.img InstallKernelModules
./rootAVD.sh system-images/android-34/google_apis_playstore/arm64-v8a/ramdisk.img InstallPrebuiltKernelModules
./rootAVD.sh system-images/android-34/google_apis_playstore/arm64-v8a/ramdisk.img InstallPrebuiltKernelModules GetUSBHPmodZ PATCHFSTAB DEBUG
./rootAVD.sh system-images/android-34/google_apis_playstore/arm64-v8a/ramdisk.img AddRCscripts
```
You should check your device version to choose the proper version
![walking]({{ site.baseurl }}/assets/images/android-studio/choose-avd-version.png)

