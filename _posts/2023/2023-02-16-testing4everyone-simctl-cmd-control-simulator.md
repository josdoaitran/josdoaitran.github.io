---
layout: post
title:  "Use Xcrun Simctl command to control simulator" 
author: testing4everyone
categories: [ tutorial, testing4everyone, course]
image: assets/images/termninal/xcrun-simctl-simulator.png
tags: [tutorial, mobile-testing]
---

# About
To control the Xcode Simulator from the command line, use the `xcrun simctl` utility, which offers commands for managing simulators (booting, shutting down, erasing, listing, etc.) and interacting with them.

# Some basic commands to control simulator

Here's a breakdown of key commands and their uses:
1. Listing Simulators:
- Command: `xcrun simctl list`
- Purpose: Displays a list of available simulators, their device types, and operating system versions.

2. Booting a Simulator:
- Command: `xcrun simctl boot <device_type>`
- Purpose: Starts a specific simulator (replace <device_type> with the desired device type, e.g., "iPhone 13 Pro").

3. Shutting Down a Simulator:
- Command: `xcrun simctl shutdown booted`
- Purpose: Shuts down all running simulators.

4. Erasing a Simulator:
- Command: `xcrun simctl erase <simulator_udid>`
- Purpose: Resets a simulator to its initial state, deleting all apps and data. You'll need to find the simulator's UDID (Unique Device Identifier) first using xcrun simctl list.

5. Simulating Hardware Controls:
- Command: `xcrun simctl <simulator_udid> <action> <value>`
- Purpose: Simulate events like changing language, locale, UI appearance, location, push notifications, background fetch, shake gesture, or device orientation.
- Examples:
`xcrun simctl set_language <simulator_udid> en` (set language to English)
`xcrun simctl set_location <simulator_udid> 37.3323 -122.0312` (set location to San Francisco)
`xcrun simctl send_push <simulator_udid> <bundle_id>` (send push notification)
`xcrun simctl shake <simulator_udid>` (simulate shake gesture)

6. Other Useful Commands:
- `xcrun simctl help`: Displays a list of all available simctl commands.
- `xcrun simctl listapps <simulator_udid>`: Lists installed apps on a simulator.
- `xcrun simctl install <path_to_ipa> <simulator_udid>`: Installs an app on a simulator.
- `xcrun simctl uninstall <bundle_id> <simulator_udid>`: Uninstalls an app from a simulator. 








