---
layout: post
title:  "Use Gemini AI supports us cover UI Testing for a Web Application"
author: donald
categories: [ web-app-test, tutorial ]
image: assets/images/ai-for-testing/ai-gemini-assistance-visual-test.png
tags: [tutorial, web-testing]
---

Idea: Use Gemini AI as an assistant to help us boost work productivity. In this post I would like to share you the way to use Gemini to help us improve UI and Visual Testing.

Boost your team's productivity and reduce the stress of UI and visual testing with the help of Gemini AI. This post will guide you through practical techniques and strategies for using Gemini to automate to generate the checklist for UI testing for a web application, improve accuracy, and ultimately, deliver higher-quality software faster.  Get ready to experience a significant leap forward in your development workflow.

# Create a simple UI checklist with Gemini 
Use Gemini to generate UI checklist to cover UI and Visual Testing
In the real project, we will have a design file example: Figma to define the designed element information, How your web application should be developed in UI view.
Due to no private disclosure, we don't have a specify UI design. I use Google search page as an example case as below image as based image.

![https://www.hubspot.com/hs-fs/hubfs/google-homepage_4.webp?width=700&height=363&name=google-homepage_4.webp](https://www.hubspot.com/hs-fs/hubfs/google-homepage_4.webp?width=700&height=363&name=google-homepage_4.webp)

I attached the Google search page screenshot to ask Gemini help me generate the checklist as bellow:

```textmate
I have a UI design for a web page as this image.
Could you provide the checklist to cover UI testing this page ?
```
And here is the result from Gemini: 

![img.png](../../assets/images/ai-for-testing/response-gemini-g-checklist-ui-test/question-response-gemini.png)

Here is the full response from Gemini as images that I captured

![response-gemini-g-checklist-ui-test-1.png](../../assets/images/ai-for-testing/response-gemini-g-checklist-ui-test/1.png)
![response-gemini-g-checklist-ui-test-2.png](../../assets/images/ai-for-testing/response-gemini-g-checklist-ui-test/2.png)
![response-gemini-g-checklist-ui-test-3.png](../../assets/images/ai-for-testing/response-gemini-g-checklist-ui-test/3.png)
![response-gemini-g-checklist-ui-test-4.png](../../assets/images/ai-for-testing/response-gemini-g-checklist-ui-test/4.png)
![response-gemini-g-checklist-ui-test-5.png](../../assets/images/ai-for-testing/response-gemini-g-checklist-ui-test/5.png)
![response-gemini-g-checklist-ui-test-6.png](../../assets/images/ai-for-testing/response-gemini-g-checklist-ui-test/6.png)
![response-gemini-g-checklist-ui-test-7.png](../../assets/images/ai-for-testing/response-gemini-g-checklist-ui-test/7.png)
![response-gemini-g-checklist-ui-test-8.png](../../assets/images/ai-for-testing/response-gemini-g-checklist-ui-test/8.png)
![response-gemini-g-checklist-ui-test-9.png](../../assets/images/ai-for-testing/response-gemini-g-checklist-ui-test/9.png)

We can see Gemini AI helps us list out of almost essential point off Visual testing for a web app.
- UI Check Layout.
- Specify UI test
- Accessibility test
- Functionality works in browser.
- Performance UI and Security.

**Note: you still need to review and update the checklist how it is relevant to your project.**

# Use Gemini to execute visual testing
After I used Gemini AI to generate the UI check-list for covering testing for a web app, I will use Gemini to execute the UI testing to cover UI check Layout and some specify UI test. Let's see How Gemini play
I captured the screenshot of Google search page in my Brave browser to compare the visual UI of base image that I did in the previous step.

Here is my request to Gemini to ask it do comparison between base image and compared image.

- Based image
  ![https://www.hubspot.com/hs-fs/hubfs/google-homepage_4.webp?width=700&height=363&name=google-homepage_4.webp](https://www.hubspot.com/hs-fs/hubfs/google-homepage_4.webp?width=700&height=363&name=google-homepage_4.webp)
- Compared image
![img.png](../../assets/images/ai-for-testing/respone-gemini-execute-ui-test/compared-image-gg.png)

- Here is my requests to Gemini:
![img.png](../../assets/images/ai-for-testing/respone-gemini-execute-ui-test/1.png)

Here is the response from Gemini to highlight the differences
![img.png](../../assets/images/ai-for-testing/respone-gemini-execute-ui-test/2.png)
![img.png](../../assets/images/ai-for-testing/respone-gemini-execute-ui-test/3.png)
![img.png](../../assets/images/ai-for-testing/respone-gemini-execute-ui-test/4.png)
![img.png](../../assets/images/ai-for-testing/respone-gemini-execute-ui-test/5.png)
![img.png](../../assets/images/ai-for-testing/respone-gemini-execute-ui-test/6.png)

# The accuracy of AI response and Security aspect 
Keep in your mind: Gemini still can make mistake !!! we have to check again and Protect the data in your project.

After I reviewed the way that Gemini returned the result. It covered the differences in browser types (Brave and Chrome in based image). Therefore, it contained the redundant comparison.

## Refine the test and adjust the test how Gemini could work better
I tried to narrow down our scope testing to ignore the differences between 2 types of browsers.

Here is my new prompt to Gemini:
![img.png](../../assets/images/ai-for-testing/refine-ask-gemini-again/prompt.png)

And here is the new response from Gemini
![img.png](../../assets/images/ai-for-testing/refine-ask-gemini-again/1.png)
![img.png](../../assets/images/ai-for-testing/refine-ask-gemini-again/2.png)
![img.png](../../assets/images/ai-for-testing/refine-ask-gemini-again/3.png)

## Ask Gemini to compare the difference rate and miss-match acceptance 
In visual testing, we should have the miss-match acceptance rate to consider the actual UI is acceptable or not.
For example, the difference rate is 8%, but the acceptance is 10%. The actual UI can be passed.

Now, I requested to Gemini to set an acceptance and give me the resul of testing.
![img.png](../../assets/images/ai-for-testing/miss-match-acceptance-gemini/chat-promtp.png)
And here is the Gemini's evaluation
![img.png](../../assets/images/ai-for-testing/miss-match-acceptance-gemini/1.png)
![img.png](../../assets/images/ai-for-testing/miss-match-acceptance-gemini/2.png)
![img.png](../../assets/images/ai-for-testing/miss-match-acceptance-gemini/3.png)
![img.png](../../assets/images/ai-for-testing/miss-match-acceptance-gemini/4.png)
![img.png](../../assets/images/ai-for-testing/miss-match-acceptance-gemini/5.png)
![img.png](../../assets/images/ai-for-testing/miss-match-acceptance-gemini/6.png)

However, the above result is not reflected to actual scenario as fixed comparison.
The language differences should be ignore here.
Let me refine it again:
![img.png](../../assets/images/ai-for-testing/miss-match-acceptance-gemini/refine/refine.png)
![img.png](../../assets/images/ai-for-testing/miss-match-acceptance-gemini/refine/1.png)
![img.png](../../assets/images/ai-for-testing/miss-match-acceptance-gemini/refine/2.png)
![img.png](../../assets/images/ai-for-testing/miss-match-acceptance-gemini/refine/3.png)
![4.png](../../assets/images/ai-for-testing/miss-match-acceptance-gemini/refine/4.png)
# Happy Testing ^^

