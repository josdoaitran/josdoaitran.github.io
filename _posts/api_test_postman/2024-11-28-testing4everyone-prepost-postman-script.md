---
layout: post
title:  "Sharing - Testing4Everyone - Postman - PreRequest & PostResponse"
author: testing4everyone
categories: [ postman, tutorial ]
image: assets/images/api-testing/postman-prerequest-postresponse.png
---

In this short post, I would like to share you the script that in a video of Testing4Everyone channel. It is related to PreRequest and PostResponse in Postman tool to generate 

<p><iframe style="width:100%;" height="515" src="https://www.youtube.com/embed/oNTV1lBDwhU?si=ZtyZVzNqYb8&lc" frameborder="0" allowfullscreen></iframe></p>

Here is the script of PreRequest
```js
function generateRandomUserName(length) {
    const characters = 'abcdefghijklmnopqrstuvwxyz0123456789';
    let result = '';
    const charactersLength = characters.length;
    for (let i = 0; i < length; i++) {
        result += characters.charAt(Math.floor(Math.random() * charactersLength));
    }
    return result;
}

function generateRandomPassword(length) {
    const characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';
    const specialCharacters = '!@#$%^&*()_+{}:<>?';
    
    let result = '';

    // Ensure at least one special character
    result += specialCharacters.charAt(Math.floor(Math.random() * specialCharacters.length));
    
    // Fill the rest of the password
    const charactersLength = characters.length;
    for (let i = 1; i < length; i++) {
        result += characters.charAt(Math.floor(Math.random() * charactersLength));
    }

    // Shuffle the result to mix the special character in
    result = result.split('').sort(() => 0.5 - Math.random()).join('');

    return result;
}

pm.environment.set("username", generateRandomUserName(7))
pm.environment.set("password", generateRandomPassword(10));



```

Here is the script of PostResponse
```js
pm.test("Save FistName and LastName value to Environment", function () {
    var jsonData = pm.response.json();
    let firstname = pm.environment.set("firstname", jsonData.firstname)
    let lastname = pm.environment.set("lastname", jsonData.lastname)
    console.log(jsonData.firstname)
    console.log(jsonData.lastname)
});
```