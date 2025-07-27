---
layout: post
title:  "Testing for your web application when 3rd party cookies will be blocked on Chrome"
author: donald
categories: [ microservice-test, collection, event-driven ]
image: assets/images/microservice-testing/monolithic-vs-microservices-architecture.png
tags: [tutorial, microservice-test, event-driven]
---

Testing for your web application when 3rd party cookies will be blocked on Chrome


# Summary

Chrome is the most popular Web browser that End-User is using to browse on a web application.

Testing for web application with Chrome browser type is always focused to assure the application working well. Especially, The new Chrome version is released, it completely impacts to the quality of your web application.

From version 121, Google Chrome will have the plan to block all Cookies of 3rd Party. You can refer to this site more: [https://developers.google.com/privacy-sandbox/blog/cookie-countdown-2024jan](https://developers.google.com/privacy-sandbox/blog/cookie-countdown-2024jan) 

[https://developers.google.com/privacy-sandbox/blog/cookie-countdown-2023oct](https://developers.google.com/privacy-sandbox/blog/cookie-countdown-2023oct)

In this post, I would like to summary and share the steps you should do in testing aspect to assure that your application will be still working well once Google Chrome block all Cookies from 3rd Party on Chrome.

Table of Content

# What is Cookies?

Cookies in Web Application:

Cookies are **small text files that a website sends to a user's browser**. They help websites remember information about a user's visit, which can make the site more useful and easier to visit again.

Cookies can store a user's preferences, session data, and other information that may help improve the overall experience on a website.

Example: Your cookies in Chrome browser

![walking]({{ site.baseurl }}/assets/images/web-testing/testing-web-application-3rd-party-cookies-be-blocked-chrome/Untitled.png)

# How 3rd Cookies can impact to your application, once 3rd Cookies is blocked

Here is the official site from Google about 3rd party cookies will be blocked in the future.

[https://developers.google.com/privacy-sandbox/3pcd](https://developers.google.com/privacy-sandbox/3pcd)

![](https://developers.google.com/static/privacy-sandbox/assets/images/blog/timeline-third-party-coo-fd786ca08c6e9_1440.png)

On the some newest chrome version, you can see the alert on Console of Chrome browser. To alert to EndUser and Developers that we should have the proper plans to handle it soon.

![walking]({{ site.baseurl }}/assets/images/web-testing/testing-web-application-3rd-party-cookies-be-blocked-chrome/Untitled 1.png)

---

> **About Testing aspect, you should have the plans to perform testing to assure that your web application testing is still working once 3rd party cookies will be blocked.
It is really important if your application integrates with a several 3rd party cookies.**
> 

# How we can perform testing

We can cover this testing by 2 ways: **Manual testing** (Enable blocked all 3rd cookies on your Chrome and Go through all features of your application) and **Automation testing** with several of automation testing framework, we can enable the mode to block all 3rd party cookie, and take advantages of automation testing to cover testing. On this post, I draft the **example code to disable 3rd party Cookies** 

## Manual testing by enable block all 3rd party on Chrome

- Open new tab on your Chrome browser  and navigate to this link:

```
chrome://flags/#test-third-party-cookie-phaseout
```

![walking]({{ site.baseurl }}/assets/images/web-testing/testing-web-application-3rd-party-cookies-be-blocked-chrome/Untitled 2.png)

We have to change the value from **Disable** to **Enable,** and restart your browser

![walking]({{ site.baseurl }}/assets/images/web-testing/testing-web-application-3rd-party-cookies-be-blocked-chrome/Untitled 3.png)

From now, you can switch enable or disable mode to allow 3rd third-party when you access to a site with these steps.

Example, I access to https://amazon.com

- Click on View Site Information of URL panel of Chrome browser

![walking]({{ site.baseurl }}/assets/images/web-testing/testing-web-application-3rd-party-cookies-be-blocked-chrome/Untitled 4.png)

Click on Cookies and site data:

![walking]({{ site.baseurl }}/assets/images/web-testing/testing-web-application-3rd-party-cookies-be-blocked-chrome/Untitled 5.png)

On this panel, you can enable again to allow 3rd cookies, It looks like however it should consider this message:

![walking]({{ site.baseurl }}/assets/images/web-testing/testing-web-application-3rd-party-cookies-be-blocked-chrome/Untitled 6.png)

**After we disable all 3rd party cookies on Chrome browser, we can execute all essential test cases to assure your web application still working well or not**

In order to verify that all 3rd party cookies are blocked or not, you can open Developer mode  and Element tab with Console. you can see the alert **“Reading third-party cookie is blocked”**

![walking]({{ site.baseurl }}/assets/images/web-testing/testing-web-application-3rd-party-cookies-be-blocked-chrome/Untitled 7.png)

## Automation testing - Launch a WebDriver with mode: block all 3rd party on Chrome

Here are some examples of how "profile.block_third_party_cookies" is used:

- Python - Selenium:
    
    ```
    "profile.block_third_party_cookies": True
    ```
    
- Serenity:
    
    ```
    "profile.block_third_party_cookies="true"
    ```
    
- Java - Selenium
    
    ```java
    // 2 ways to block 3rd party cookies
    // Option 1
    options.addArguments("--block-third-party-cookies");
    // Option 2
    
    Map<String, Object> prefs = new HashMap<>();
    prefs.put("profile.block_third_party_cookies", true);
    options.setExperimentalOption("prefs", prefs);
    WebDriver driver = new ChromeDriver(options);
    ```
    

You can follow these above patterns on your test script or test framework. Then you execute all essential test cases to verify the main functionality of your application.

# Bonus 🙂

How to fix the issue if your application has the troubles once the 3rd party cookies be blocked by browser

Refer to this site: [https://developers.google.com/privacy-sandbox/3pcd](https://developers.google.com/privacy-sandbox/3pcd) Google Developer suggests the way to migrate to privacy preserving solutions

![walking]({{ site.baseurl }}/assets/images/web-testing/testing-web-application-3rd-party-cookies-be-blocked-chrome/Untitled 8.png)

Examples cases with Error

![walking]({{ site.baseurl }}/assets/images/web-testing/testing-web-application-3rd-party-cookies-be-blocked-chrome/Selected_January_28_2024_123243.png)

![walking]({{ site.baseurl }}/assets/images/web-testing/testing-web-application-3rd-party-cookies-be-blocked-chrome/Selected_January_28_2024_123046.png)

![walking]({{ site.baseurl }}/assets/images/web-testing/testing-web-application-3rd-party-cookies-be-blocked-chrome/Selected_January_28_2024_123119.png)

![walking]({{ site.baseurl }}/assets/images/web-testing/testing-web-application-3rd-party-cookies-be-blocked-chrome/Selected_January_28_2024_123141.png)