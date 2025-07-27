---
layout: post
title:  "How to use AI (Gemini) to generate test cases and test data"
author: donald
categories: [ ai-test, tutorial ]
image: assets/images/ai-for-testing/how-ai-chatgpt-generate-test-data-write-auto-performance-test/Untitled 3.png
tags: [tutorial, ai-for-testing]
---

How to use AI (Gemini) to generate test cases and test data

# Overview

- Gemini AI comes from Google. It supports us with the way like Copilot Microsoft, OpenAI Chat GPT.
- Gemini AI: [https://gemini.google.com/app](https://gemini.google.com/app)

# Problems and example demands

We will ask Gemini with this question and given context, and expect that to receive the valuable information Gemini AI

## Scenario 1

Give the as much information as much as possible as below

```latex
 Let’s imagine that we are testing an authentication form which includes username and password fields. 
 There are some requirements which:
- A password and a username should fulfill: 
- The username must be at least 4 characters but not more than 15 and can include letters and numbers.
- The password must be at least 8 characters and contain at least one letter and one number or special character. 
The password can not be the same as the username. 
Could you generate test cases and test data to cover above requirement
```

**A password and a username should fulfill**
- The **username** must be:

- **At least 4 characters** but **not more than 15**
- include letters and numbers.

- The **password** must be

- **At least 8 characters.**
- contain **at least one letter** and one number or special character. 
The password can not be the same as the username.

![walking]({{ site.baseurl }}/assets/images/ai-for-testing/how-to-use-gemini-to-generate-test-cases-and-data/Untitled.png)

**Here is the results that I copied from the response from Gemini as below**

I'd be glad to generate test cases and test data to cover the authentication form requirements:

**Username Validation**

| **Test Case ID** | **Description** | **Test Data (Username)** | **Expected Result** |
| --- | --- | --- | --- |
| TC-U-01 | Valid username (4 characters, letters & numbers) | user1234 | Username accepted |
| TC-U-02 | Valid username (15 characters, letters & numbers) | veryLongUsername | Username accepted |
| TC-U-03 | Username less than 4 characters | user12 | Username rejected (error message: "Username must be at least 4 characters") |
| TC-U-04 | Username more than 15 characters | ThisIsAUsernameThatIsTooLong | Username rejected (error message: "Username must be less than 16 characters") |
| TC-U-05 | Username with special characters | user!@# | Username rejected (error message: "Username can only contain letters and numbers") |

**drive_spreadsheetExport to Sheets**

**Password Validation**

| **Test Case ID** | **Description** | **Test Data (Password)** | **Expected Result** |
| --- | --- | --- | --- |
| TC-P-01 | Valid password (8 characters, letters & numbers) | Password123 | Password accepted |
| TC-P-02 | Valid password (8 characters, letters & special characters) | Password!@ | Password accepted |
| TC-P-03 | Valid password (more than 8 characters, letters & numbers) | VeryLongPassword123 | Password accepted |
| TC-P-04 | Password less than 8 characters | pass123 | Password rejected (error message: "Password must be at least 8 characters") |
| TC-P-05 | Password without letters or numbers (only special characters) | !@#$%^&* | Password rejected (error message: "Password must contain at least one letter and one number or special character") |
| TC-P-06 | Password matching username (case-sensitive) | user1234 | Password rejected (error message: "Password cannot be the same as the username") |
| TC-P-07 | Password matching username (case-insensitive) | User1234 (username: user1234) | Password rejected (error message: "Password cannot be the same as the username") |

**Additional Test Cases (Optional)**

- Test behavior with empty username or password fields.
- Verify password masking (asterisks or dots) when entering the password.
- Test "Remember Me" functionality (if applicable).
- Test error handling for invalid characters or unexpected input.
- Simulate scenarios with network issues or server timeouts during authentication.

**Notes:**

- You can adjust the error message examples to match the specific wording used in your application.
- Consider adding test cases for specific password complexity requirements (e.g., minimum number of uppercase and lowercase letters, special characters).
- These test cases cover basic functionality; expand them based on your application's specific features and security needs.

## Scenario 2

We expect AI help us generate more test data when we do some testing cases

```latex
Generate 5 fake vietnamese name to test sign-up new account with this field:
- first name: no more than 10 characters, no special characters
- last name: no more than 8 characters, no special characters
```

![walking]({{ site.baseurl }}/assets/images/ai-for-testing/how-to-use-gemini-to-generate-test-cases-and-data/Untitled 1.png)

We require more conditions for AI, we expect that AI return the answer how it meets 2 techniques for design test cases: (boundary techniques and equivalent techniques)

```latex
Generate 5 fake vietnamese name to test sign-up new account with this field.
How we can cover all essential test cases (boundary techniques and equivalent techniques)
- first name: no more than 10 characters, no special characters
- last name: no more than 8 characters, no special characters
```

Here is the response from Gemini

Here are 5 fake Vietnamese names that you can use to test sign-up for a new account:

1. First Name: Linh, Last Name: Cao (4 characters each)
2. First Name: Mai Anh, Last Name: Tran (7 characters for first name, 4 characters for last name)
3. First Name: Hoai, Last Name: Nguyen (4 characters each, common Vietnamese last name)
4. First Name: Nam Phuong, Last Name: Le (10 characters for first name, 2 characters for last name)
5. Dan, Quach (Both 1 syllable names, short and common)

These names cover various scenarios for testing the sign-up field:

- **Short names (under 5 characters)**
- **Long names (up to 10 characters)**
- **Double names (first name with two words)**
- **Common Vietnamese last names**
- **One-syllable names**

By testing with these names, you can ensure that the sign-up field can handle different lengths and formats of Vietnamese names.

**Boundary and Equivalence Testing Techniques**

- **Boundary testing** involves testing the system at the edges of its specified input range. In this case, you would test names with exactly 1 character, 5 characters (middle of the allowed range), and 10 characters (maximum allowed length) for the first name, and similar tests for the last name (up to 8 characters).
- **Equivalence testing** involves testing the system with input values that are expected to be valid or invalid based on the specifications. Here, you would test valid names following the format (letters only), names with spaces (expected to be valid for double names), and names with special characters (expected to be invalid).

By combining these techniques with the sample names provided, you can thoroughly test the sign-up field's ability to handle Vietnamese names.