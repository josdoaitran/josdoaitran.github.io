---
layout: post
title:  "How to use test data with  CSV file in JMeter"
author: donald
categories: [ performance-test, jmeter, tutorial ]
image: assets/images/performance-testing/performance-test-client-view-server-view.png
---

# Example Scenario testing that using CSV file with JMeter
In this post, we share us the way to control testing data in CSV file in JMeter tool to perform testing scenario.

In the real scenario, we need to simulate our requests as the real user with several test data such as each request has a data of user about credential. The data of all testing user will be saved as a CSV file.

Therefore, we consider to use JMeter to pick up 1 data to insert into each request of sample.

# Steps to use CSV Data config to insert the proper data into each request in JMeter

## Step 1: Save the test data as csv
Example we save the test data as this file: `lesson_19_user_data.csv`
- We assume that we have a CSV file has contents like:
```
email, password
9l07jgxo@example.com, de24214ew@!$
penapi2@mailinator.com, penapi2
```
## Step 2: Add the CSV data config element into our Test Plan script.
Go Add >> Config Elements >> CSV Data Set Config

## Step 3: Select the file director of your CSV file
![](https://i.ibb.co/s9fdqDdS/csv-data-set-config-select-file.jpg)

## Step 4: Configuring the variable and mapping to the data of csv file
Base on the column name of your CSV file, we configure our variable in our JMter script properly. In this tutorial, we use the column 1 to save the user email and colum 2 to save the password.

Therefore, I will set the value of Variable Names (comma-delimited) field as: `email, password`. Then, our JMeter test script will contain 2 variable `${email}` and `${password`

## Step 5: Configure the variable in sample properly.
After set up the variable will be saved in `CSV Data Set configure`, we will update the variable in sampler properly as bellow:

![](https://i.ibb.co/8LfMHPSf/set-variable-csv-data-set-config.jpg)

## Ignore first line

In JMeter, "Ignore First Line" refers to a setting within the "CSV Data Set Config" element, which allows you to skip the first line of a CSV file if it contains headers or information you don't want to use as test data, essentially treating the first line as column names instead of data values to be used in your test; you would typically set this option to "True" if you want to ignore the first line of the CSV file.

## Delimiter in JMeter

- To specify a tab as the delimiter in JMeter, use the escape sequence "\t" within the "Delimiter" field of the "CSV Data Set Config" element.
- This essentially means that whenever you want to separate data values in your CSV file with a tab character, use "\t" to indicate it in JMeter settings.

For example, we have the csv with content:

```
Name    Age    City
John	30    New York
Jane	25    London
```
We should configure the value of our CSV Data Set Config as bellow:
Delimiter: `"\t"` instead of using `,`
Variable Names: `"Name", "Age", "City"`


## When we set the value of Allow quoted data as True?
Allow quoted data? If your values can contain commas, and you also use commas as delimiters, then allow quoted values. 
Example: If a value can be "123 Main street, Springfield", make sure to surround it by double quotes and enable this option, otherwise it will be split into two columns.

- In my example, our data doesn't include comas therefore I set the value as False.

## How about `Recycle on EOF` field and `Stop thread on EOF`?
EOF aka Ending of File. 2 fields enable us control our test, when the event of reading at the end of our csv file.

- Recycle on EOF: To make the file re-read from the beginning on reaching the end of file (EOF). The default value is true. 

- Stop thread on EOF: This option will stop the thread if reaches to end of the file (EOF). The default value is false

## Sharing Mode in CSV Data Set Config
It depends on where we add our CSV Data Set Config.
- Add a CSV Data Set Config in a JMeter Test Plan, and Set the value of Sharing Mode as All threads. Then all VUser in JMeter Test Plan will pick data on CSV file to do testing
- Add a CSV Data Set Config in a Thread Group and Set the value of Sharing Mode as Current Thread Group. All VUser in Thread Group will pcik data on CSV file to do testing.
- Add a CSV Data Set Config in a Thread Group and Set the value of Sharing Mode as current thread. Only 1 thread pick up data on CSV file 


