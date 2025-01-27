---
layout: post
title:  "Performance test - Preprocessor and Postprocessor in JMeter"
author: donald
categories: [ performance-test, tutorial ]
image: assets/images/performance-testing/performance-test-client-view-server-view.png
---

# Situational Cases
In the real scenarios, there are many cases which require us to do some pre-condition or tear-down steps in each request or sampler in JMeter. They are aka: Preprocessor and Postprocessor in JMeter.

## Preprocessor in JMeter
- A "preprocessor" is an element that executes actions before a sampler request is sent, allowing you to modify request settings or update variables prior to sending the request.
- Preprocessors happen before a request is made

### Example Preprocessor - (User Parameters 

### Example Preprocessor - JSR223 Preprocessor)


## PostProcessor in JMeter
- A "postprocessor" executes actions after a sampler request is received, enabling you to process the response data, like extracting specific values from it;
- And postprocessors happen after a response is received.
