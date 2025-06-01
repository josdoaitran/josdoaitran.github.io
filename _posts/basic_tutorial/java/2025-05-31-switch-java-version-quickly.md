---
layout: post
title:  "Install Multi Java Version in a Mac machine and switch Java Version quickly" 
author: testing4everyone
categories: [ tutorial, smart-testing-lab, course]
image: assets/images/basic-tutorial/java/switch-java-version-mac.png
tags: [tutorial, java]
---

I am lazzzzy and I don’t remember the original command line exactly to switch Java versions when each workspace will work with specify Java version. How it is proper to each workspace.
Then, I tried to write some bash script in my `zprofile` to change to rememberable command in terminal to change Java version quickly.

Update these scripts in your `zprofile` or `zshrc` or `bash_profile`

![walking]({{ site.baseurl }}/assets/images/basic-tutorial/java/switch-java-version-mac.png)

```aiignore
list_java_versions(){
    echo "<3 <3 <3 <3 List of Java version in my machine <3 <3 <3"
    /usr/libexec/java_home -V
}

switch_to_java_version(){
    JAVA_VERSION=$1
    export JAVA_HOME=`/usr/libexec/java_home -v "$JAVA_VERSION"` && echo "Successfully Switched to Java $JAVA_VERSION" || echo "Failed, check Java Version again"
}
```