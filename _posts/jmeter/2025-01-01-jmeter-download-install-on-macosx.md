---
layout: post
title:  "Performance test - Download and Install JMeter On MacOSX and Windows machines"
author: donald
categories: [ performance-test, jmeter, tutorial ]
image: assets/images/performance-testing/performance-test-jmeter-basic-course.png
---

JMeter - Download and Install On MacOSX and Windows machines
In order to install and run JMeter in MacOSX or Windows, We need to assure that our computer already installed Java or not

# Check Java on your computer

To Check whether your machine installed Java or not yet.

**Windows**

Open command line:

```bash
java -version
```

**MacOSX**

Open your terminal and run this command:

```bash
java --version
```

![walking]({{ site.baseurl }}/assets/images/performance-testing/jmeter-download-install-on-macosx/Untitled.png)
# Download JMeter

- We navigate the official site Apache JMeter to download JMeter.

[https://jmeter.apache.org/](https://jmeter.apache.org/)

- Navigate to download page, via Download Release link on main menu or this URL: [Link](https://jmeter.apache.org/download_jmeter.cgi)
- Select the binaries editor to download instead of selecting the Source editor.

(If you choose Source editor, you need to run build the source code to compile to jar file and open the JMeter successfully.)

- Extract the binary as zip file that we downloaded.

# Open JMeter

From the binaries folder, we access to `{source_folder}/bin file`. And open the JMeter tools by:

- On MacOSX: We run file: `Jmeter.sh` with command: `sh jmeter.sh`
- On Windows: We run file `Jmeter.bat`

![walking]({{ site.baseurl }}/assets/images/performance-testing/jmeter-download-install-on-macosx/Untitled 1.png)