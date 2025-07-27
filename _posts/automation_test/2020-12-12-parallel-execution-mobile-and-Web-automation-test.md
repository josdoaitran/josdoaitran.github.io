---
layout: post
title:  "Parallel Execution - Mobile and Web automation test without Cloud Devices Service [Updating]"
author: donald
categories: [ sharing, automation-test ]
image: assets/images/software-testing-general/software-testing-tools.jpg
---

Once your project has the large number of test cases in automated of E2E testing, you will have demands for parallel executions for your automated test framework.

- E2E test takes us much efforts, implement time cost, and specially execution times.
- You always expect that your test scripts will run faster to get the test reports sooner. That's also a key point to get success in Continuous testing in Agile or DevOps Model.

Following to these above demands, there were many technical designs for automated test frameworks to make test framework execution be optimized.

On this post, I would like to mention 2 mains approaches, that we usually apply on our projects for executing test parallel.

Probably, it will be easier for us to be able run parallel if we purchase commercial tools for cloud services such as: Device Farm - AWS, Browser Stack, LambdaTest, ...

![walking]({{ site.baseurl }}/assets/images/automation-test/parallel-execution-mobile-and-Web-automation-test/Untitled.png)
## Selenium Grid - Trail path of thinking in Parallel test execution

- One of the most favorite framework test design for parallel execution is **Selenium Grid**. Almost of test projects and test framework are be applied.

What is Selenium Grid ? => You can refer more here: https://www.selenium.dev/documentation/grid/

- For multiple Browsers - Web Application Testing - Parallel Execution:

![walking]({{ site.baseurl }}/assets/images/automation-test/parallel-execution-mobile-and-Web-automation-test/Untitled 1.png)

- For multiple Devices - Mobile application Testing - Parallel Execution:

![walking]({{ site.baseurl }}/assets/images/automation-test/parallel-execution-mobile-and-Web-automation-test/Untitled 2.png)
**Multi-threading to run Parallel test execution**