---
layout: post
title:  "Performance test - Preprocessor and Postprocessor in JMeter"
author: donald
categories: [ performance-test, tutorial ]
image: assets/images/performance-testing/performance-test-client-view-server-view.png
---

# Situational Cases
In the real scenarios, there are many cases which require us to do some pre-condition or tear-down steps in each request or sampler in JMeter. They are aka: Preprocessor and Postprocessor in JMeter.

## Preprocessor in JMeter
- A "preprocessor" is an element that executes actions before a sampler request is sent, allowing you to modify request settings or update variables prior to sending the request.

- Preprocessors happen before a request is made

### Example Preprocessor - User Parameters 
We have the question: `When we should use User parameters in JMeter?` 

#### User parameters could be considered as a Dynamic Data Assignment:
- When each thread in your test requires unique data (e.g., usernames, passwords, or other test parameters).
- For example, if you’re simulating multiple users logging into a system, you can assign a unique username and password to each thread.

#### User parameters could be considered as a data collections 
- You use this preprocessor when the variables need to be initialized or updated before the sampler runs. For example, if your HTTP request depends on variables set in the User Parameters.
- When you want to parameterize your test without using CSV Data Set Config.
- For instance, you can define variables directly within the User Parameters, eliminating the need for external files.

#### User parameters could be used as Testing Unique Scenarios:
- When testing scenarios like account creation or user-specific data updates where each thread needs a unique identifier.
- Each sample request should used an unique data.

#### How to add an User parameter
- As below image, we can add an User parameter.
![](https://i.ibb.co/FDDxG0P/preprocessor-adding-user-parameters.jpg)
- An User parameters
![](https://i.ibb.co/tXj5cDZ/user-parameters-example.jpg)

#### Example Use Case with User parameters
Suppose you’re testing a login API for 10 users. Each user should have a unique username and password.
1.	Add a Thread Group with 10 threads.
2.	Add the User Parameters Preprocessor:
- Set variables:
- username: `user_${__threadNum}`
- password: `pass_${__threadNum}`
3. Use `${username}` and `${password}` in your HTTP Request.
By using the User Parameters Preprocessor, each thread will have a unique set of values for username and password.
- Update the variable in sampler request to configuration
![](https://i.ibb.co/6snCgYc/user-parameters-in-sampler-request.jpg)

### Example Preprocessor - JSR223 Preprocessor
The JSR223 Preprocessor in JMeter is used when you need to execute custom scripting or logic before a sampler is executed. It provides powerful customization capabilities for test scenarios that go beyond the standard JMeter components. You can write scripts in supported languages like `Groovy`, `JavaScript`, `Jython`, or `Beanshell`, with `Groovy` being the most commonly used due to its efficiency and performance.

`When we should use JSR223 Preprocessor in JMeter?`

1.	Dynamic Request Preparation:
- When you need to dynamically modify or generate request data before it is sent to the server.
- Example: Generating a unique token, calculating a checksum, or encrypting a value for use in the request.

2.	Custom Logic for Preprocessing:
- When you need to execute custom logic or transformations that aren’t natively supported by JMeter components.
- Example: Reformatting JSON or XML data before sending it.

3.	Correlation:
- Extracting or manipulating data from previous responses to use in the current sampler’s request.
- Example: Using a session ID or dynamic token retrieved from a prior request.

4.	Advanced Parameterization:
- When you need to generate complex or computed test data that cannot be easily managed using CSV Data Set Config or User Parameters.
- Example: Generating a timestamp, hashing a value (e.g., MD5, SHA-256), or creating a random string with specific rules.

5.	Condition-Based Execution:
- When certain preprocessing actions are required only under specific conditions.
- Example: Setting specific headers based on the thread number or previous response values.

6.	Performance Optimization:
- Groovy in JSR223 Preprocessors is faster than other scripting options (e.g., Beanshell or JavaScript), making it suitable for performance-critical operations.

#### How to add a JSR223 Preprocessor
- As below image, we can add a JSR223 Preprocessor.
![](https://i.ibb.co/tJkxq9c/jsr223-add-jsr-preprofessor.jpg)

- An example JSR223 to generate Dynamic data
![](https://i.ibb.co/nRMqLvb/example-jsr-preprocessor-generate-dynamic-data.jpg)
- Thank to JSR223 Preprocessor, we can write a scrip to populate the data of a field before we trigger the request.

#### Some example script that we can use JSR223 Preprocessor

- Generating Dynamic Data for the Request
```groovy
// Generate a unique timestamp
def timestamp = System.currentTimeMillis()
vars.put("timestamp", timestamp.toString())
```

- Adding a Custom Header with an Encrypted Token
```groovy
import java.util.Base64
String username = "user1"
String password = "pass123"
String token = Base64.getEncoder().encodeToString((username + ":" + password).getBytes())
sampler.addNonEncodedArgument("", "", "")
sampler.getHeaderManager().add("Authorization", "Basic " + token)
```

- Modifying the Request Body
```groovy
String requestBody = vars.get("originalBody")
String updatedBody = requestBody.replace("PLACEHOLDER", "newValue")
vars.put("updatedBody", updatedBody)
```
Use ${updatedBody} in your HTTP Request.

- Correlation: Extract and Use Data
```groovy
String response = prev.getResponseDataAsString()
String token = response.find(/"token":"(.*?)"/)[1]
vars.put("token", token) 
```
Use ${token} in the next request.
- Generate the random email
```groovy
def allowedChars = ('a'..'z') + ('0'..'9')
def randomString = (1..8).collect { allowedChars[new Random().nextInt(allowedChars.size())] }.join()
def emailDomain = "example.com"
def randomEmail = "${randomString}@${emailDomain}"
vars.put("randomEmail", randomEmail)
log.info("Generated Random Email: ${randomEmail}")
```

## PostProcessor in JMeter

- A "postprocessor" executes actions after a sampler request is received, enabling you to process the response data, like extracting specific values from it;
- And postprocessors happen after a response is received.

### Example Postprocessor - JSON extractor

The JSON Extractor PostProcessor in JMeter is used to extract specific values or elements from a JSON response after a request is executed. 
This is particularly useful when working with APIs that return data in JSON format, as it allows you to retrieve dynamic values (like session IDs, tokens, or user data) for further use in your test.
We have the question: `When we should use Postprocessor - JSON extractor in JMeter?`

1.	Extracting Values from JSON Responses:
To extract dynamic values like tokens, session IDs, or any field values from an API’s JSON response.

2.	Chaining API Requests:
To pass the extracted value (e.g., an id or token) from one request to another.

3.	Dynamic Test Data:
When testing APIs that return unique or user-specific data, you can extract these values dynamically.

4.	Validation or Assertions:
You can use extracted values for assertions to validate specific conditions (e.g., status codes or specific field values).

#### Example scenario:

- We have 2 sampler request
- 1st request to login and receive the response, it contains the token value.
- 2nd request will be based on the token value of 1st request to get the user-info.

![](https://i.ibb.co/Qp7dVCR/example-json-extractor-postprocessor.jpg)

#### Fields in Json Extractor in JMeter provides us:

- **Name of created variable**: The variable name that will store the extracted value(s). Example: `token`, `userId`.
- **JSON Path expressions**: The JSON path to extract the desired value. Example: `$.token`, `$.data.id`.
- **Match No**: Defines which match to return if there are multiple matches:  0 for all, 1 for the first match, etc.
- **Default Value**: The value to use if no match is found. Example: NOT_FOUND.

#### JSON Path Syntax Overview

It works as Expression
- `$.field`: Extracts the value of a specific field.
- `$.field.subfield`: Extracts a nested field value.
- `$..field`: Extracts all matching fields at any level.
- `$.field[*].subfield`: Extracts a subfield from all items in an array.

Example: We have the Sample JSON Response from the 1st request.

```json
{
  "status": "success",
  "data": {
    "userId": 12345,
    "token": "abc123xyz",
    "roles": ["admin", "editor"]
  }
}
```

Configuration:
- Variable Names: userId, token, roles
- JSON Path Expressions:
- $.data.userId → Extracts 12345.
- $.data.token → Extracts abc123xyz.
- $.data.roles[0] → Extracts admin.

Result:
- ${userId} → 12345
- ${token} → abc123xyz
- ${roles} → admin

### Example Postprocessor - JSR223 PostProcessor
- The JSR223 PostProcessor in JMeter is used to execute custom scripts after a sampler’s response has been received. 
- It allows you to process the response, extract data, or perform custom logic that isn’t natively supported by JMeter components. It is highly versatile and efficient when written in Groovy, which is the recommended scripting language for JMeter.

We have the question: `When we should use Postprocessor - JSR223 PostProcessor in JMeter?`

1. Custom Correlation (Dynamic Data Extraction):
- When you need to extract specific dynamic values from a response that cannot be handled by native extractors like the JSON Extractor, Regular Expression Extractor, or XPath Extractor.
- Example: Extracting multiple dynamic values from a complex or irregular JSON, XML, or HTML response.

2. Debugging:
- To log or inspect specific parts of the response for debugging purposes.
- Example: Printing a part of the response to the logs for troubleshooting.

3. Data Preparation for Further Use:
- When you need to process or format data extracted from the response for use in subsequent requests.
- Example: Encrypting a value, formatting a timestamp, or concatenating multiple extracted values.

4. Custom Validations and Assertions:
- When you want to verify specific aspects of the response and set a pass/fail status for the sampler based on custom conditions.
- Example: Checking if a certain value in the response meets a specific threshold.

#### Example use-case with JSR Postprocessor

1. Extracting Multiple Values from JSON:
If the response is complex and the JSON Extractor can’t handle it:
```groovy
import groovy.json.JsonSlurper

def response = prev.getResponseDataAsString()
def json = new JsonSlurper().parseText(response)
def token = json.data.token
def userId = json.data.userId

vars.put("token", token)
vars.put("userId", userId)
```

2. Setting Custom Assertions

```groovy
def response = prev.getResponseDataAsString()
if (!response.contains("expectedValue")) {
    AssertionResult.setFailure(true)
    AssertionResult.setFailureMessage("Expected value not found in response.")
}
```

3. Extracting Data from HTML Response:

If the response contains HTML and you need to extract a specific value:

```groovy
def response = prev.getResponseDataAsString()
def matcher = response =~ /<input name="csrfToken" value="(.*?)">/
if (matcher.find()) {
    vars.put("csrfToken", matcher.group(1))
} 
```

4. Logging for Debugging:
```groovy
log.info("Response: " + prev.getResponseDataAsString())
log.info("Response Time: " + prev.getTime()) 
```

#### Example scenario:
- We have 2 sampler request
- 1st request to login and receive the response, it contains the token value.
- 2nd request will be based on the token value of 1st request to get the user-info.
![](https://i.ibb.co/5cT8yDX/example-jsr223-postprocessor.jpg)