---
layout: post
title:  "Configure AmazonQ & CodeWhisperer AWS AI tools for Software Engineer"
author: donald
categories: [ tips, sharing ]
image: assets/images/software-development/open-vscode-terminal/Untitled.png
---
Configure AmazonQ & CodeWhisperer AWS AI tools for Software Engineer
# 🕹️Summary

In this post, I would like to summary and share with you the essential steps to take advantages of Amazon AI tools - Amazon CodeWhisperer for daily works of a Software Engineer.

Software Engineer usually use the well-know Editor tool such as: IntelliJ, Pycharm of JetBrain, or Visual Studio Code, … Then, On this note page, I will take them as the example tools, when I apply to use CodeWhisperer.

Table of Content

# 🌈 Amazon Q

[https://aws.amazon.com/blogs/aws/introducing-amazon-q-a-new-generative-ai-powered-assistant-preview/](https://aws.amazon.com/blogs/aws/introducing-amazon-q-a-new-generative-ai-powered-assistant-preview/)

Amazon Q - AI Assistance Chat tool.

You can use Amazon Q to have conversations, solve problems, generate content, gain insights, and take action by connecting to your company’s information repositories, code, data, and enterprise systems. Amazon Q provides immediate, relevant information and advice to employees to streamline tasks, accelerate decision-making and problem-solving, and help spark creativity and innovation at work.

# 🌈 CodeWhispere ?

## What is Amazon CodeWhisperer

Amazon CodeWhisperer is one of tools from AWS, that they provide machine learning-powered code generator that provides you with code recommendations in real time. 

As you write code, CodeWhisperer automatically generates suggestions based on your existing code and comments. Your personalized recommendations can vary in size and scope, ranging from a single line comment to fully formed functions.

In oder to get more information from official document from Amazon CodeWhisperer: [https://docs.aws.amazon.com/codewhisperer/latest/userguide/what-is-cwspr.html](https://docs.aws.amazon.com/codewhisperer/latest/userguide/what-is-cwspr.html)

![](https://thiagoalves.ai/images/codewhisperer/cover-codewhisperer.png)

Suggested Code for these programming languages: [https://docs.aws.amazon.com/codewhisperer/latest/userguide/language-ide-support.html](https://docs.aws.amazon.com/codewhisperer/latest/userguide/language-ide-support.html)

- Java
- Python
- JavaScript
- TypeScript
- C#
- Go
- PHP
- Rust
- Kotlin
- SQL

The Infrastructure as Code (IaC) languages with the most support are:

- JSON (AWS CloudFormation)
- YAML (AWS CloudFormation)
- HCL (Terraform)
- CDK (Typescript, Python)

CodeWhisperer also supports code generation for:

- Ruby
- C++
- C
- Shell
- Scala

***Amazon CodeWhisperer*** provides us 2 options:

- Personal Purpose / Individual Tier CodeWhisperer
- Enterprise Purpose for an Organization (Company) - Code Whisperer Professional

## Pricing - CodeWhisperer

[https://docs.aws.amazon.com/codewhisperer/latest/userguide/billing.html](https://docs.aws.amazon.com/codewhisperer/latest/userguide/billing.html)

# 📑 Configuration CodeWhisperer

As tutorial post, this post will be mentioned with Personal purpose configuration steps for initializing setup CodeWhisperer Vs Code and JetBrains with **AWS Builder ID login.**

### Prerequisite

Probably, You need to have an AWS Account to use Amazon CodeWhisperer. In cases, you are working on your company and use AWS account that your company provided you. You have to align with your manager and request to enable Code Whisperer on your account.

In order to sign-up an AWS account, you can refer to this site and follow the on-boarding steps to have an AWS account: [https://aws.amazon.com/resources/create-account/](https://aws.amazon.com/resources/create-account/)

And y***ou sign-in your AWS Account on your default browser application on your computer via this link***: 
[Link To Sign-in AWS Account](https://signin.aws.amazon.com/signin?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3FhashArgs%3D%2523%26isauthcode%3Dtrue%26nc1%3Df_ct%26src%3Dfooter-signin%26state%3DhashArgsFromTB_eu-north-1_0a30a4663d630901&client_id=arn%3Aaws%3Asignin%3A%3A%3Aconsole%2Fcanvas&forceMobileApp=0&code_challenge=zztlBkYRaIfS8d_MtQFOQbQwR2a8ZlS30yEUdcER5CQ&code_challenge_method=SHA-256)

This step is deeply important to sign-in your AWS Account via AWS BuilderID for AWS Toolkit

### Configure AWS plugin / extension

We need to install AWS Toolkit plugin or Extension on your Editor Code (Visual Code and JetBrain)

- Visual Code: [https://code.visualstudio.com/](https://code.visualstudio.com/)
- Jetrain: IntelliJ, PyCharm: [https://www.jetbrains.com/idea/](https://www.jetbrains.com/idea/)

AWS ToolKit for Visual Code: [https://marketplace.visualstudio.com/items?itemName=AmazonWebServices.aws-toolkit-vscode](https://marketplace.visualstudio.com/items?itemName=AmazonWebServices.aws-toolkit-vscode)

AWS ToolKit for JetBrain InteljI: [https://aws.amazon.com/intellij/](https://aws.amazon.com/intellij/)

Visual Code

![walking]({{ site.baseurl }}/assets/images/software-development/configure-amazonq-codewhisperer-aws-ai/Untitled.png)
JetBrain - Editor Tool

![walking]({{ site.baseurl }}/assets/images/software-development/configure-amazonq-codewhisperer-aws-ai/Untitled 1.png)

Configure your AWS Account on AWS Toolkit

Open AWS Toolkit on the left menu of Visual Code

![walking]({{ site.baseurl }}/assets/images/software-development/configure-amazonq-codewhisperer-aws-ai/Untitled 2.png)

You can see the AWS Get-Started UI

![walking]({{ site.baseurl }}/assets/images/software-development/configure-amazonq-codewhisperer-aws-ai/Untitled 3.png)

On AWS Q + CodeWhisperer, you click on Processed to Browser

![walking]({{ site.baseurl }}/assets/images/software-development/configure-amazonq-codewhisperer-aws-ai/Untitled 4.png)

Click on Open,

![walking]({{ site.baseurl }}/assets/images/software-development/configure-amazonq-codewhisperer-aws-ai/Untitled 5.png)

Your browser will REQUIRE login your AWS account, and redirect to this site. Then click on Confirm and Continue button

![walking]({{ site.baseurl }}/assets/images/software-development/configure-amazonq-codewhisperer-aws-ai/Untitled 6.png)

You have to configure AWS Builder ID, in case you never configure AWS Builder ID before.

![walking]({{ site.baseurl }}/assets/images/software-development/configure-amazonq-codewhisperer-aws-ai/Untitled 7.png)

Input Multi-verification Code will be sent to your email

![walking]({{ site.baseurl }}/assets/images/software-development/configure-amazonq-codewhisperer-aws-ai/Untitled 8.png)

You will input the password for creating a new AWS Builder

and see the Confirm popup, confirm and you can see the successful message such as:

![walking]({{ site.baseurl }}/assets/images/software-development/configure-amazonq-codewhisperer-aws-ai/Untitled 9.png)

Then, we can see your AWS Toolkit

![walking]({{ site.baseurl }}/assets/images/software-development/configure-amazonq-codewhisperer-aws-ai/Untitled 10.png)

Now, we get Started to use Amazon Q and Amazon CodeWhisperer

![walking]({{ site.baseurl }}/assets/images/software-development/configure-amazonq-codewhisperer-aws-ai/Untitled 11.png)

On JetBrain, we also open AWS Toolkits on the left menu of Jetbrain

![walking]({{ site.baseurl }}/assets/images/software-development/configure-amazonq-codewhisperer-aws-ai/Untitled 12.png)

You can see the AWS Get-Started UI on your JetBrain Editor Tool

***If you are going to use AWS SSO and configured in your company. You can follow these steps***

![walking]({{ site.baseurl }}/assets/images/software-development/configure-amazonq-codewhisperer-aws-ai/Untitled 13.png)

Click on Sign-in Get Started on CodeWhisperer

![walking]({{ site.baseurl }}/assets/images/software-development/configure-amazonq-codewhisperer-aws-ai/Untitled 14.png)

You click on Processed to Browser.

Navigate to web browser,

![walking]({{ site.baseurl }}/assets/images/software-development/configure-amazonq-codewhisperer-aws-ai/Untitled 15.png)

And Confirm to login SSO successfully, it will redirect to AWS Console.

***To use personal account, on AWS Toolkit you navigate to Explorer tab***

And you can see the AWS Tookit UI looks like UI on Visual Code

![walking]({{ site.baseurl }}/assets/images/software-development/configure-amazonq-codewhisperer-aws-ai/Untitled 16.png)

Then, you can see the same steps on ToolKit of Visual Code, we can setup AWS Builder account and login AWS Builder, by click on **Authentication** button or **ReAuthentication** (I logged in when I were composing this post)

Using Amazon Q, Click on Chat with Q to use Amazon Q chatbot

![walking]({{ site.baseurl }}/assets/images/software-development/configure-amazonq-codewhisperer-aws-ai/Untitled 17.png)

Amazon Whisperer

On Authenticate with AWS Toolkit, we click on **Use For Free with AWS Builder ID**

![walking]({{ site.baseurl }}/assets/images/software-development/configure-amazonq-codewhisperer-aws-ai/Untitled 18.png)

![walking]({{ site.baseurl }}/assets/images/software-development/configure-amazonq-codewhisperer-aws-ai/Untitled 19.png)

Using your BuilderID to login 

![walking]({{ site.baseurl }}/assets/images/software-development/configure-amazonq-codewhisperer-aws-ai/Untitled 20.png)

![walking]({{ site.baseurl }}/assets/images/software-development/configure-amazonq-codewhisperer-aws-ai/Untitled 21.png)

Generate the example code

![walking]({{ site.baseurl }}/assets/images/software-development/configure-amazonq-codewhisperer-aws-ai/Untitled 22.png)

# Reference

- **CodeWhisperer article**: [https://aws.amazon.com/blogs/aws/amazon-codewhisperer-free-for-individual-use-is-now-generally-available/](https://aws.amazon.com/blogs/aws/amazon-codewhisperer-free-for-individual-use-is-now-generally-available/)
- **Amazon CodeWhisperer coding in Python with VS Code:** [https://dev.to/aws-heroes/amazon-codewhisperer-for-data-science-and-analytics-get-started-with-generative-ai-on-aws-part-2-5e66](https://dev.to/aws-heroes/amazon-codewhisperer-for-data-science-and-analytics-get-started-with-generative-ai-on-aws-part-2-5e66)
- **AWS- CodeWhisperer Workshop**:
    - Code [https://github.com/aws-samples/amazon-codewhisperer-workshop](https://github.com/aws-samples/amazon-codewhisperer-workshop)
    - Site: [https://aws.amazon.com/blogs/devops/develop-a-serverless-application-in-python-using-amazon-codewhisperer/](https://aws.amazon.com/blogs/devops/develop-a-serverless-application-in-python-using-amazon-codewhisperer/)

                                   — Copyright 2024 — 