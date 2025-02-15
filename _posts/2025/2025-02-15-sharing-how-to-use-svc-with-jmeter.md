---
layout: post
title:  "How to use test data with  CSV file in JMeter"
author: donald
categories: [ performance-test, tutorial ]
image: assets/images/performance-testing/performance-test-client-view-server-view.png
---

# Example Scenario testing that using CSV file with JMeter
In this post, we share us the way to control testing data in CSV file in JMeter tool to perform testing scenario.

In the real scenario, we need to simulate our requests as the real user with several test data such as each request has a data of user about credential. The data of all testing user will be saved as a CSV file.

Example:

```
sigupEmail, username
penapi1@mailinator.com, penapi1
penapi2@mailinator.com, penapi2
```

Therefore, we consider to use JMeter to pick up 1 data to insert into each request of sample.

# Steps to use CSV Data config to insert the proper data into each request in JMeter

## Step 1: Save the test data as csv
Example we save the test data as this file: `lesson_19_user_data.csv`

## Step 2: Add the CSV data config element into our Test Plan script.
