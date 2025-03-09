---
layout: post
title:  "Main keys to learn Mobile Application Testing - Appium"
author: donald
categories: [ mobile-app-test, tutorial, appium ]
image: assets/images/mobile-testing/automation-testing/appium.png
---

# The essential key points for Mobile Application Testing - Appium

I received the question from my audiences about `How to learn Mobile Application with Appium`
In this post, I would like to list out all essential points that you can learn and gain the new skills in Appium via 2 ways
- From my experiences, I did self-learn from everything in the Internet
- From free and open AI tutor :), ChatGPT (Open AI). I asked ChatGPT as new bie and received the suggestions from ChatGPT. We can compare to choose the proper plan for each guy. 

From my comments, you could have your ideas to select a proper plan for yourself to learn new skills with Appium.
Instead of depended on any guy (your instructor, your line manager, even me)

## My suggestion to learn Mobile automation test with Appium
Here is my answer, it was collected from my knowledge and skills

![](https://lh7-us.googleusercontent.com/pSy9m0xuJCgmttavS62h7dA0Mg9GJFTjFBa2_lzjf0MVyRAS3Pc9rO8ivEjyS2L03_5zR5kXIyyVkyUAV84rQ4mYv0OBtG7mHS4llQVH6TSx-_DNS7OzNhwMSrdRDLCqP3Ow3TsPe0Ns9pFBJqIQSj8)

## Point 1: What is Appium, Understand how Appium works
- Open source tools, enable us  cover automated test for mobile app (Android, IOS), Mobile Web App and Windows application.
- It can be controlled and worked with modern programming languages: Java, Python, Javascript, Typescript, C#, ...
- If we use Java, We can integrate Appium and TestNG or JUnit framework to build a mobile automation test framework.
- How Appium Works: Appium Server, Appium Client, How we can control a mobile app device via Appium.
What is Appium Inspector app ?
- What is  W3C WebDriver protocol
- Appium 1.0 and Appium 2.0 ?
You can refer to: [https://appium.io/docs/en/2.0/guides/migrating-1-to-2/](https://appium.io/docs/en/2.0/guides/migrating-1-to-2/)

or this page: 
[https://www.lambdatest.com/blog/appium-inspector-for-apps/](https://www.lambdatest.com/blog/appium-inspector-for-apps/)

- Appium 1.0: Support these protocols: `W3C WebDriver` & `JSON Wire Protocol`.
- Appium 2.0: Support these protocols: `W3C WebDriver` only, No support: `JSON Wire Protocol` more.
- Appium 1.0 capability like:
```
{
  "platformName": "Android",
  "platformVersion": "11.0",
  "deviceName": "emulator-5554",
  "app": "/path/to/your/app.apk",
  "automationName": "UiAutomator2"
}
```

- Appium 2.0 capability like:

```
{
  "appium:platformName": "Android",
  "appium:platformVersion": "11.0",
  "appium:deviceName": "emulator-5554",
  "appium:app": "/path/to/your/app.apk",
  "appium:automationName": "UiAutomator2"
}
```

- Updating a specific driver in Appium 2.0: `uiautomator2`, `XCUITest` driver.

## Point 2: Setup a local environment to work with Appium
- Install NodeJS (The NodeJS environment is required to run Appium)
- Install Appium Server (Appium App)
- Install Appium Inspector.
- Use Appium Inspector to inspect element 
- Connect a virtual device to Appium
- Android Device Emulator and iOS simulator
- Inspect a specify app via app package in a mobile device from Appium.

## Point 3: Understanding of Locator with Appium
- Type: ID
- Type: Xpath and Xpath locator syntax
- Type: Class Name
- Type: AccessibilityID
- Type: UIAutomation for android only
- Type: iOS Predicate String for iOS only
- Type: iOS Class Chain for iOS only

## Point 4: Build up a basic test script to control mobile application
- Initialize a maven Java project
- Add Appium and TestNG dependencies.
- Write a method to initialize driver to connect to mobile device.
- Specially, How to use Appium Inspector to compare the performance of each types of locator
- How use Wait method in Appium
- Basic actions to elements in Appium: Click, SendKey with Appium.

## Point 5: Apply Some essential features of a test framework
- Apply POM model ~ Basic design pattern
- Including Log4J / Logback for test framework
- Initialize HTML report with TestNG or using other library to generate reports

## Point 6: Integrate with CI or Multi-Device testing with Cloud Devices
- Run test via CI tool: Jenkins
- Run test with Cloud Devices: Sauce Labs, BrowserStack, Lambda Test.
- Parallel execution with TestNG.
- Distributed testing Execution instead of Parallel test Execution In Test Framework

## Point 7: Build test framework with BDD
- Integrate Cucumber into Test Framework
- Write test in BDD
- Hook, Glue in BDD with Appium
- Cucumber report and generate HTML report

## Point 8: Some special cases in Appium
- Special action: Swipe up, down, left, right
- Handle Face ID: Passed /Failed action
- Handle Touch ID: Passed / Failed
- Handle injecting capture image from camera.
- Handle popup to accept permissions in device (Android / iOS)
- Handle Push Notification in Device

## ChatGpt answered the question "Please help me list out of the essential key points for Mobile Application Testing - Appium"
Here is my question to Open AI, ChatGPT:

```angular2html
"Please help me list out of the essential key points for Mobile Application Testing - Appium"
```
And here is the answer from ChatGPT
![walking]({{ site.baseurl }}/assets/images/mobile-testing/automation-testing/chatgpt-appium-automation-p1.png)
![walking]({{ site.baseurl }}/assets/images/mobile-testing/automation-testing/chatgpt-appium-automation-p2.png)
![walking]({{ site.baseurl }}/assets/images/mobile-testing/automation-testing/chatgpt-appium-automation-p3.png)
![walking]({{ site.baseurl }}/assets/images/mobile-testing/automation-testing/chatgpt-appium-automation-p4.png)

I really liked the tutorial ChatGPT provided on Appium lesson suggestion. It covered everything from scratch to the basic levels, preparing us to complete important tasks in automated testing for a mobile application.

However, it did mention the essential points:
- Compare to Appium 1.0 and Appium 2.0 has the many chances. 
- Appium 2.0 not support `JSON Wire Protocol` more
- Appium 2.0 driver plugin: `UIAutomator2`, `XCUITest` driver
- How we can set up an Android device emulator and iOS simulator.
- Inspect a specify app via app package in a mobile device from Appium.
- I did NOT mention a specify programming language that I want to  learn in a mobile automation test course. Therefore, ChatGPT did not mention the essential steps that we should learn with a test framework.
- From my experiences, I suggest we should apply distributed execution instead of parallel execution in test. It helps us easier to debug the test than using parallel execution.

There are two points that I would really love AI to suggest improvements on my post: `Performance & Network Testing` and `Regularly cleaning device cache/data before test execution`. Some of these points impact the stability of mobile automation testing, and one point relates to flaky testing.
And especially about, we must install: Android SDK for Android and Xcode for iOS to run automation test for android and ios devices.

[//]: # ([![10 keys for web application testing #shorts #mobile]&#40;https://img.youtube.com/vi/cYTZdLm1uxI/0.jpg&#41;]&#40;https://www.youtube.com/watch?v=cYTZdLm1uxI&#41;)
[//]: # ()
[//]: # ()
[//]: # ([![Testing4Everyone - 10 keys for web application testing - giải thích chi tiết]&#40;https://img.youtube.com/vi/sUCE_sctluE/0.jpg&#41;]&#40;https://www.youtube.com/watch?v=sUCE_sctluE&#41;)
[//]: # ()
