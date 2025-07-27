---
layout: post
title:  "How to automate API an User login if the authentication of application is using AWS Auth - Cognito"
author: donald
categories: [ microservice-test, collection, event-driven ]
image: assets/images/microservice-testing/monolithic-vs-microservices-architecture.png
tags: [tutorial, microservice-test, event-driven]
---

How to automate API an User login if the authentication of application is using AWS Auth - Cognito

## Cognito AWS Auth

You can refer to this link: [AWS Cognito](https://www.blogger.com/blog/post/edit/1444050721395049955/1068879068876984399#)

https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html

![walking]({{ site.baseurl }}/assets/images/microservice-testing/how-to-automate-api-user-login-aws-cognito/Untitled.png)
assets/images/microservice-testing/how-to-automate-api-user-login-aws-cognito/Untitled.png

## Automated test script to login app with Cognito:

In order to do E2E automated test script for your application with Auth Cognito AWS, we follow Cognito Guide from AWS.

https://docs.aws.amazon.com/cognito-user-identity-pools/latest/APIReference/API_InitiateAuth.html

Before we implement more test scripts to cover testing for internal function of your app, you need to login your app by your credential information, then you can have the token of your test-account.

The below command in CURL command helps you to make an auth request to AWS Cognito to get account token.

![walking]({{ site.baseurl }}/assets/images/microservice-testing/how-to-automate-api-user-login-aws-cognito/Untitled 1.png)

```java
curl --location --request POST 'https://cognito-idp.{{region}}.amazonaws.com/' \
--header 'Content-Type: application/x-amz-json-1.1' \
--header 'X-Amz-Target: AWSCognitoIdentityProviderService.InitiateAuth' \
--data-raw '{
    "AuthParameters" : {
        "USERNAME" : {{username}},
        "PASSWORD" : {{password}}
    },
    "AuthFlow" : "USER_PASSWORD_AUTH",
    "ClientId" : {{client_id}}
}'
```

---

                                   — Copyright 2024 — 