---
layout: post
title:  "How to configure Open a project in Visual Code from terminal"
author: donald
categories: [ tips, sharing ]
image: assets/images/software-development/open-vscode-terminal/Untitled.png
---
# How to configure Open a project in Visual Code from terminal

Owner: josdoaitran
Verification: Verified
Tags: Tips
Date: February 12, 2024

In this post, I share with you the way to work more effectively to open a project on Visual Code when we are working on Terminal.
In real scenario, after we just cloned a new repository via Terminal, you can use this open Terminal console to open the project in Visual Code to save time instead doing more steps (Open Visual Code and using Open Menu to point out the directory of new repository that we expect to open).

In order to do that, we have to do some essential steps on the first time we open a folder on Visual Code from Terminal.

Open Visual Code, we can use this hot-key to open Prompt: 

- `Command + Shift + P` on Mac
- `Control + Shift + P` on Windows

Then, we input the value “Shell” to search “***Shell Command: Install `Code` command in PATH***”

For instance,

![walking]({{ site.baseurl }}/assets/images/software-development/open-vscode-terminal/Untitled.png)

We click on “***Shell Command: Install `Code` command in PATH***”

![walking]({{ site.baseurl }}/assets/images/software-development/open-vscode-terminal/Untitled 1.png)

Click on Ok button to setup Code value on Path of your terminal profile.

Then, we can see this message

![walking]({{ site.baseurl }}/assets/images/software-development/open-vscode-terminal/Untitled 2.png)

From now, we can use our terminal to open any folder from Terminal

For example, I am going to open this folder `selenium-everything`, I will access my terminal to this folder and run this command:
`code .`

Beside that, we also open the project or folder on Visual Code editor from anywhere, by this command:
`code .\home\test\selenium-everything\`

                                   — Copyright 2024 — 
