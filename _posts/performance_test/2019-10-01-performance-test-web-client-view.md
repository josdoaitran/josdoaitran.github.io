---
layout: post
title:  "[Tutorial] Performance test - Web application - Client View"
author: donald
categories: [ performance-test, tutorial ]
image: assets/images/performance-testing/performance-test-client-view-server-view.png
---

Performance test is the non-functional test,  one of points in non-functional testing view for Web Application is End-User's behavior Optimization. It's really important in digital environments web application, eCommerce web application, .... to deliver the best value to customers. We should not only care the availabilities of Web application's functions but also high performance of web application. It helps us keep in customer's mind good views and impression about your products.

There are many factors affect to performance of your products. To narrow down, we will focus on monitoring the performance of a web application in Client View.

There are many factors from client side and they impact to performance of your web application:

- Location of client
- Network speed of client
- Your application is applied CDN or not ?
- Your web application is applied Minify or not? ([https://raidboxes.io/en/blog/hosting-performance/reduce-minify-css-html-javascript/](https://raidboxes.io/en/blog/hosting-performance/reduce-minify-css-html-javascript/))
- Your frontend of your application consume much CPU, RAM, Battery, ... or not

In this documents, I would like share some cases that we can consider to evaluate the performance of your product:

- **How fast your web application load ? (We don't consider the number of concurrent user accessing to your product.)**
- **Use web application monitoring to evaluate your web application ? (Using CDN or not, ...)**
- **How much the frontend of your application consume the CPU/ RAM of client's device (Computer, Mobile)**

Web Application monitoring tool as client view:

We can use Web application monitoring tools and they show various metrics and technical parameters affecting the page load speeds and user experience. Example: check website status or uptime and track critical indicators such as page size, time to first byte, broken links, CPU /RAM utilization, and more.

Here is the list of applications that we can use to check the performance of your product in client view:

**1. https://gtmetrix.com/**

![walking]({{ site.baseurl }}/assets/images/performance-testing/performance-test-web-client-view/Untitled.png)

**2. https://www.webpagetest.org/**

![walking]({{ site.baseurl }}/assets/images/performance-testing/performance-test-web-client-view/Untitled 1.png)

Example: https://guesthouseshop.com/about

Script to do example steps with Webpagetest.org:

```json
logdata 0
navigate    http://store.nike.com/us/en_us/
sendClickAndWait    class=login-text
setValue    data-componentname=emailAddress yourEmailAddress@eg.com
setValue    data-componentname=password yourPassword
clickAndWait    value=LOG IN
logdata 1
navigate    http://store.nike.com/us/en_us/
```

Reference

- [https://www.tek-tools.com/apm/web-monitoring-tools-and-tips](https://www.tek-tools.com/apm/web-monitoring-tools-and-tips)
- Client View and Server View:

![walking]({{ site.baseurl }}/assets/images/performance-testing/performance-test-client-view-server-view.png)

                                   — Copyright 2024 — 