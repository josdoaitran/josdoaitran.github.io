---
layout: post
title:  "Tips - How to enable LogCli Pytest on Pycharm"
author: donald
categories: [ pytest, tips ]
image: assets/images/software-development/pytest-config-pycharm.png
---

Pycharm is a Editor tool for Python and be developed by Jetbrain team. Pycharm with 2 license options: Community and Progressional editor. So, it and Visual Code is selected as a favorite editor tools for Python Developer.

In many cases, we apply Pytest to cover our several testing purposes: Unit test, Automation Test, … And to capture the log better, we can apply Logger and Logging library on Python.

However, we we run our tests on Pycharm. On default configuration, Pycharm disable log text in **LogCli.** Then, we can NOT see the log if we run tests on Edit Configuration features.

In this note, I would like to share with you the cases to edit configuration on your Pycharm how it works with our test frameworks or your project.

On Run/Debug configuration of your project, you can update Additional Arguments this value:
(Depends on your target, you can adjust your log level: Info, …)

```
--log-level=DEBUG -o log_cli=True -o log_cli_level=DEBUG
```

![walking]({{ site.baseurl }}/assets/images/software-development/pytest-config-pycharm.png)
