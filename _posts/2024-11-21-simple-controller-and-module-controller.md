---
layout: post
title:  "Essential points of Sampler Controller, Module Controller, Test Fragment, Include controller."
author: testing4everyone
categories: [ Jekyll, tutorial ]
image: assets/images/performance-testing/simple-controller-modular-controller-in-jmeter.png
---

# Sampler Controller and Module Controller
Context:
You want to group sampler/requests together, easier to reuse and maintain again all your samplers.

We order our Samplers in a specify scenario such as:
+ Sign-up / register
+ Sign-in (Using again and repeatable)
+ Flight Booking


## Sampler Controller

- To group some sampler or requests into a simple controller.
- Easy to manage all requests / samplers in a feature or functions of an application.
![](https://i.ibb.co/wp738kY/simple-controller-in-jmeter.jpg)

## Module Controller in JMeter

- Support us to control group of requests should be run before run other group of requests.
- Example: We should run some requests for accessing /home and /login before run some requests for adding items to carts, purchasing your order
![](https://i.ibb.co/F5H473f/modular-controller-in-jmeter.jpg)

## Test Fragments
- Simmilar to Simple Controller, however it will be disable default.
- It is used to collect sample like a simple test controller.
- We can use modular to invoke samples in a test-fragment instead of using simple controller. It helps us easier to manage our sampler in our test plan.
- We can export a sampler as a Test Fragment and save as a JMeter file. Then, we can import a test fragment into a JMeter test plan.
How to add a test fragment
![](https://i.ibb.co/d0psmrw/create-a-test-fragment.jpg)
![](https://i.ibb.co/S60fFYG/test-fragment-is-default-disable.jpg)

## Export a sampler as a Test Fragment file

![](https://i.ibb.co/Qct6ryZ/export-a-sampler-as-a-test-fragment.jpg)
## Include controller
- We can use include controller to import any test fragment as a jmeter file

![](https://i.ibb.co/zXBCRzV/include-controller-import-test-fragment.jpg)

- It helps us to reuse the sampler from other test fragment.
- In a project, we can maitain all sampler in all test plans easily and effectively.

## Reference lists
Here is the list of offical links from JMeter
- Sampler Controller: https://jmeter.apache.org/usermanual/component_reference.html#Simple_Controller
- Module Controller: https://jmeter.apache.org/usermanual/component_reference.html#Module_Controller


[//]: # (## Full HTML)

[//]: # ()
[//]: # (Perhaps the best part of Markdown is that you're never limited to just Markdown. You can write HTML directly in the Markdown editor and it will just work as HTML usually does. No limits! Here's a standard YouTube embed code as an example:)

[//]: # ()
[//]: # (<p><iframe style="width:100%;" height="315" src="https://www.youtube.com/embed/Cniqsc9QfDo?rel=0&amp;showinfo=0" frameborder="0" allowfullscreen></iframe></p>)