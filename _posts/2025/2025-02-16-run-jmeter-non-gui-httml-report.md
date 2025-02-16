---
layout: post
title:  "How to use test data with  CSV file in JMeter"
author: donald
categories: [ performance-test, tutorial ]
image: assets/images/performance-testing/performance-test-client-view-server-view.png
---

Run JMeter via Commandline - NonGUI jmeter mode and HTML report
GUI JMeter will consume more resources. Therefore, we usually use JMeter in NonGUI mode in run test scenario.
Otherwise, we completely integrate JMeter in integration tools such as: Jenkins, JMeter with Docker, ...
### How to run JMeter script in non-gui mode and view test result in JMeter mode.

- Step 1: Navigate to `jenkin-source` folder and `/bin` folder
  ![](https://i.ibb.co/q2ZTJkn/natigate-jmeter-bin-folder.jpg)
  ![](https://i.ibb.co/v6sWcmt3/list-out-all-files-jmeter-folder.jpg)
- Step 2: Run the command as bellow format
```
jmeter -n -t {location_of_jmeter_file} -l {location of the result file}
```
For example, we can run the command with several OS and export as `CSV file`
- Windows
```
jmeter -n -t C:/path/to/your/test.jmx -l C:/path/to/results/report-file.csv
```
- Linux / Macoxs
```
jmeter.sh -n -t /path/to/your/test.jmx -l /path/to/results/report-file.csv
```
- Besides, we can run these command to refer more params or receive the information of helper in Jmeter commandline
  `jmeter -h` or `jmeter -?`

Run my example Jmeter script
![](https://i.ibb.co/S4DbRVkW/run-jmeter-example-in-mac.jpg)

### Run a JMeter script and save as `.jtl` file and use Graph element to diplay as a chart.
- Instead of save the test result as CSV file, we can save as a JTL file and use chart listener to visualise all test result to debug or analysis test reports.

`jmeter.sh -n -t /path/to/your/test.jmx -l /path/to/results/report-file.jtl`

For example:
```
sh jmeter.sh -n -t /Users/doaitran/Documents/personal/coding/jmeter-for-api-and-perrformance-test/basic_lessons/lesson_20_csv_in_jmeter.jmx -l /Users/doaitran/Documents/personal/coding/jmeter-for-api-and-perrformance-test/basic_lessons/lesson20-result.jtl
```

And we can back to our JMeter test plan in GUI mode, and add a Graph listener element and browser to JTL file to visual our test report as a chart.

![](https://i.ibb.co/wNMmcxrF/adding-graph-listener-browser-jtl-file.jpg)

![](https://i.ibb.co/W42tRT6G/display-chart-from-jtl-report-file.jpg)

### Generate html report Jmeter
Otherwise, JMeter has a pram in jmeter command to export the result as html folder
```
jmeter.sh -n -t /path/to/your/test.jmx -l /path/to/results/report-file.csv -e -o /path/to/results/html-report
```

For example
```
sh jmeter.sh -n -t /Users/doaitran/Documents/personal/coding/jmeter-for-api-and-perrformance-test/basic_lessons/lesson_20_csv_in_jmeter.jmx -l /Users/doaitran/Documents/personal/coding/jmeter-for-api-and-perrformance-test/basic_lessons/lesson20-result.csv -e -o /Users/doaitran/Documents/personal/coding/jmeter-for-api-and-perrformance-test/basic_lessons/lesson20-html-report
```
![](https://i.ibb.co/2Ys88FCG/run-jmeter-non-gui-html-report.jpg)

Then we can get the html report folder as below image and we can open as this step
![](https://i.ibb.co/B5PttjMw/open-report-html-on-report-folder.jpg)

And here is an example html displayed in my browser.
![](https://i.ibb.co/QFQXbCNP/html-report-jmeter.jpg)