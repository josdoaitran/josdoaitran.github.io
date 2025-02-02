---
layout: post
title:  "If Controller in JMeter"
author: donald
categories: [ jmeter, tutorial ]
image: assets/images/performance-testing/if-controller-in-jmeter.png
---
>If Controller is one of the most important controllers. In JMeter, the "If Controller" is used to execute its child elements only when a specified condition evaluates to true. To evaluate all child elements under the "If Controller," we can use a combination of a condition and well-designed child elements.

Here’s an example:

Scenario: Execute All Children If a Condition is True
Suppose we want to execute three HTTP requests under the "If Controller" only if a variable executeCondition is set to "true".

Test Plan Structure
```angular2html
Test Plan
- Thread Group
    If Controller (Condition: ${executeCondition} == "true")
        - HTTP Request 1
        - HTTP Request 2
        - HTTP Request 3
```
## Steps to Create This:
### Step 1: Add a Thread Group:
- Right-click the Test Plan → Add → Threads (Users) → Thread Group.
### Step 2: Add a User Defined Variables:
- Right-click the Thread Group → Add → Config Element → User Defined Variables.
- Add a variable, e.g., executeCondition, and set its value to true.
### Step 3: Add an If Controller:
- Right-click the Thread Group → Add → Logic Controller → If Controller.
- Set the condition to `${executeCondition} == "true`.
### Step 4: Add HTTP Request Samplers:
- Right-click the If Controller → Add → Sampler → HTTP Request.
- Create three HTTP requests (or any other child elements).

## Example 
Here I give you the example cases to practice the condition scripting:
In the If Controller's "Condition" field, you would enter:
```groovy
${__groovy(vars.get("userType") == "admin")}
```
This condition checks if the variable executeCondition is equal to "true". If the condition evaluates to true, all child HTTP Request samplers will execute.

Output Example:
- If executeCondition = true: JMeter runs HTTP Request 1, HTTP Request 2, and HTTP Request 3.
- If executeCondition = false: JMeter skips all child elements under the "If Controller."
Notes:
- Ensure proper scoping of variables to avoid conflicts.
- Use Debug Sampler to verify variable values during test runs.

![https://i.ibb.co/rssFbGg/if-controller-condition.jpg](https://i.ibb.co/rssFbGg/if-controller-condition.jpg)

## Explain about: Evaluate for All Children option
The "Evaluate for All Children" option in JMeter's If Controller determines how the condition is evaluated when the controller has multiple child elements. Here's a detailed explanation with examples of what happens when this option is checked or unchecked:

Scenario Setup:
You want to execute some child elements (e.g., HTTP Requests) under an If Controller based on a condition, and you want to observe how enabling or disabling "Evaluate for All Children" impacts execution.

We have the example Test Plan
```angular2html
Thread Group
    User Defined Variables
    myVar = 1
    If Controller (Condition: ${myVar} < 3)
    HTTP Request 1
    HTTP Request 2
```
### When "Evaluate for All Children" is Unchecked (Default Behavior)
- The condition is evaluated once when the If Controller is reached.
- If the condition evaluates to true, all children are executed sequentially.
- If the condition evaluates to false, none of the children are executed.
Example:
- Initial Value of myVar: 1.
- Condition: ${myVar} < 3.

Execution Flow:

1. The condition ${myVar} < 3 is evaluated when the If Controller is reached:
`True (1 < 3).`
2. Both HTTP Request 1 and HTTP Request 2 are executed.
3. If myVar is updated by one of the child elements (e.g., a PostProcessor modifies it), the new value does not affect the execution of subsequent children.

### When "Evaluate for All Children" is Checked
- The condition is evaluated before each child is executed.
- If the condition becomes false during execution (e.g., due to a variable update), subsequent children are skipped.
Example:
- Initial Value of `myVar: 1`.
- Condition: `${myVar} < 3.`

Execution Flow:

1. The condition ${myVar} < 3 is evaluated before executing HTTP Request 1:
True (1 < 3), so HTTP Request 1 is executed.
2. Suppose HTTP Request 1 updates myVar to 4 (e.g., using a PostProcessor or JSR223 script).
3. The condition is re-evaluated before executing HTTP Request 2:
False (4 < 3), so HTTP Request 2 is skipped.

## Use Case Examples:
- Unchecked: Use this when you want a consistent execution of all children once the condition is met, regardless of variable changes during execution.
- Checked: Use this when you want dynamic behavior where children are skipped if the condition changes during execution.
