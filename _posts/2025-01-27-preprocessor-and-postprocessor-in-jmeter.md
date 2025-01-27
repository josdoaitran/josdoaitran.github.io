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

### Example Preprocessor - User Parameters 
We have the question: `When we should use User parameters in JMeter?` 
#### User parameters could be considered as a Dynamic Data Assignment:
•	When each thread in your test requires unique data (e.g., usernames, passwords, or other test parameters).
•	For example, if you’re simulating multiple users logging into a system, you can assign a unique username and password to each thread.
#### User parameters could be considered as a data collections 
- You use this preprocessor when the variables need to be initialized or updated before the sampler runs. For example, if your HTTP request depends on variables set in the User Parameters.
- When you want to parameterize your test without using CSV Data Set Config.
- For instance, you can define variables directly within the User Parameters, eliminating the need for external files.
#### User parameters could be used as Testing Unique Scenarios:
- When testing scenarios like account creation or user-specific data updates where each thread needs a unique identifier.
- Each sample request should used an unique data.
### Adding an User parameter
- As below image, we can add an User parameter.
![](https://i.ibb.co/FDDxG0P/preprocessor-adding-user-parameters.jpg)
- 


### Example Preprocessor - JSR223 Preprocessor


## PostProcessor in JMeter
- A "postprocessor" executes actions after a sampler request is received, enabling you to process the response data, like extracting specific values from it;
- And postprocessors happen after a response is received.
