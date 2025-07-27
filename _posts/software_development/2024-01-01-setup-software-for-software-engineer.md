---
layout: post
title:  "Setup Software for Software Engineer (DEV / QA / DEV in Test) on MacOSX"
author: donald
categories: [ tips, sharing ]
image: assets/images/software-development/my-awesome-terminal-on-macbook/Untitled 1.png
---

On this page, I would like to share to everyone the essential tools that we should have on your Macbook if we are software engineer


# HomeBrew

- [https://brew.sh/](https://www.blogger.com/blog/post/edit/1444050721395049955/259010701687421121#)
- Run by this command:

```bash
/bin/bash -c "$(curl -fsSL <https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh>)"
```

# iterm2

Using this command to install

```bash
brew install --cask iterm2
```

# Install Firefox by brew

Using these commands

```bash
brew tap homebrew/cask-versions
brew install --cask firefox-developer-edition
```

# Rectangle

[https://rectangleapp.com/](https://www.blogger.com/blog/post/edit/1444050721395049955/259010701687421121#)

```jsx
brew install --cask rectangle
```

# stats

[https://github.com/exelban/stats](https://www.blogger.com/blog/post/edit/1444050721395049955/259010701687421121#)

```jsx
brew install stats
```

# Docker

[https://www.docker.com/](https://www.blogger.com/blog/post/edit/1444050721395049955/259010701687421121#)

```jsx
brew cask install docker
```

# Visual Studio Code

```jsx
brew install --cask visual-studio-code
```

# Java

Download from this source:

 
https://www.openlogic.com/openjdk-downloads?field_java_parent_version_target_id=416&field_operating_system_target_id=431&field_architecture_target_id=All&field_java_package_target_id=All

List out all java version, we installed on your MAC:

```bash
/usr/libexec/java_home -V

Matching Java Virtual Machines (2):
    11.0.16 (x86_64) "OpenLogic-OpenJDK" - "OpenLogic-OpenJDK 11" /Library/Java/JavaVirtualMachines/openlogic-openjdk-11.jdk/Contents/Home
    1.8.0_342 (x86_64) "OpenLogic-OpenJDK" - "OpenLogic-OpenJDK 8" /Library/Java/JavaVirtualMachines/openlogic-openjdk-8.jdk/Contents/Home
/Library/Java/JavaVirtualMachines/openlogic-openjdk-11.jdk/Contents/Hom
```

Check current Java version:

```bash
java --version
```

Switch Java version:

```jsx
export JAVA_HOME=`/usr/libexec/java_home -v 1.8.0_342`
or
export JAVA_HOME=`/usr/libexec/java_home -v 11.0.16`
```

# Python

install Python and setup Python on MAC:

[https://www.python.org/](https://www.blogger.com/blog/post/edit/1444050721395049955/259010701687421121#)

# Mave

Install Maven via HomeBrew:

```jsx
brew install maven
```

# NodeJS

- Install Nodejs via HomeBrew
- Command:

```bash
brew install node
```

Appium

- Install Appium Non-UI, Appium as library in Nodejs
- Command

```bash
npm install -g appium
```

• Install Appium GUI

```bash
brew install --cask appium
```

Or download DMG file: [https://github.com/appium/appium-desktop](https://github.com/appium/appium-desktop) If you get any troubles while launching Appium, you can run this command: 

```bash
xattr -cr Appium-UI.app
```

Appium Inspector

Install [https://github.com/appium/appium-inspector](https://github.com/appium/appium-inspector) 

Using homebrew:

```bash
brew install --cask appium-inspector
```