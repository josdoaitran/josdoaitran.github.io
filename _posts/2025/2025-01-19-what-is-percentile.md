---
layout: post
title:  "Performance test - What is a Percentile?"
author: donald
categories: [ performance-test, tutorial ]
image: assets/images/performance-testing/performance-test-client-view-server-view.png
---
A percentile is a statistical measure that indicates the value below which a given percentage of observations in a data set falls. For example:

The 50th percentile (or median) is the value below which 50% of the data points lie.
The 90th percentile is the value below which 90% of the data points are located, meaning 90% of the values are less than or equal to this number, and 10% are greater.
Percentiles are used to understand the distribution and spread of data, especially when the data is skewed or when you want to measure performance at different points in the data set.

# Percentile in Performance Testing

In performance testing, percentiles are used to analyze and report how a system performs for a certain percentage of users or requests, especially when looking at response times (latency) or throughput. They help identify how most users experience the system's performance, and they can show outliers or anomalies in the data.

## Key Percentiles in Performance Testing:
1. 50th Percentile (P50):
   Also known as the median, it indicates the response time below which 50% of the requests are served. It represents the "typical" performance experienced by users.

2. 90th Percentile (P90):
   It indicates that 90% of the requests were completed within this time, meaning the response time for 90% of users is better than or equal to this value, and the slowest 10% of requests took longer than this.

3. 95th Percentile (P95):
   It tells you that 95% of the requests are completed within this time. This is a commonly used metric for performance SLAs (Service Level Agreements) since it excludes the extreme outliers (5% of the slowest responses).

4. 99th Percentile (P99):
   This is the response time below which 99% of the requests are served. It captures the worst-case performance for nearly all users, highlighting rare but critical slowdowns.

## Why Percentiles Matter in Performance Testing?
Percentiles provide a more granular view of performance than average response times, especially when dealing with variability or outliers. Average (mean) response times can be misleading because a few very slow responses can skew the results, making the system look slower or faster than it actually is for most users.

For example: If 90% of your users have response times around 1 second, but 10% experience a 10-second delay, the average response time may appear acceptable (like 2 seconds), while in reality, a significant number of users are experiencing poor performance.

By looking at the 90th percentile, you can see that most users (90%) experience a response time below a certain threshold, helping you understand the system's real performance for the majority of users.

## Example in Performance Testing:
Let's say you are testing a web application, and the response times for requests are recorded. If your test results show: 50th percentile (P50): 200 ms 90th percentile (P90): 400 ms 95th percentile (P95): 600 ms 99th percentile (P99): 1 second This means:

50% of the requests are completed in 200 ms or less. 90% of the requests are completed in 400 ms or less. 95% of the requests are completed in 600 ms or less. 99% of the requests are completed in 1 second or less. This helps you see how your application performs for most users and where the performance bottlenecks or slow requests are occurring.

## How Percentiles are Used in JMeter?
In tools like Apache JMeter, percentiles are typically displayed in reports, and they help you evaluate your system's performance. JMeter calculates percentiles for response times to give a clear picture of how long it takes for a certain percentage of requests to complete.

The Aggregate Report or Summary Report in JMeter provides metrics like 90th percentile, which can be used to assess if your system meets the performance criteria for most users.
