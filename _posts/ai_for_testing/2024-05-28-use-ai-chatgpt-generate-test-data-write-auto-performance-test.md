---
layout: post
title:  "Use AI (Chatgpt) to generate test data and write automation and performance test"
author: donald
categories: [ ai-test, tutorial ]
image: assets/images/ai-for-testing/how-ai-chatgpt-generate-test-data-write-auto-performance-test/Untitled 3.png
tags: [tutorial, ai-for-testing]
---

Use AI (Chatgpt) to generate test data and write automation and performance test

# Overview

In case, I need to have the automation test script to generate a lot of users data for covering testing a sign-up API. Besides that, I am going to write a performance test script to test sign-up API with [**Locust**](https://locust.io/) - **An open source load testing tool**

I will take advantaged of the AI model on [**Chatgpt**](https://chatgpt.com/) to help me complete these tasks.

# Generate several testing data from Simple Users data

```latex
{
    "username": "john123",
    "password": "P124321@654645",
    "first_name": "John",
    "last_name": "Smith",
    "phone": "(555) 123-4567",
    "address": "123 Main St, Anytown, USA"
}
```

I inquired Chatgpt to generate 2O American user following the simple data as bellow

```latex
generate 20 American users such a simeple user infromation such as:
{
    "username": "john123",
    "password": "P124321@654645",
    "first_name": "John",
    "last_name": "Smith",
    "phone": "(555) 123-4567",
    "address": "123 Main St, Anytown, USA"
}
```

![walking]({{ site.baseurl }}/assets/images/ai-for-testing/how-ai-chatgpt-generate-test-data-write-auto-performance-test/Untitled .png)

Even, I requested Chatgpt help me format the response as a JSON file.

![walking]({{ site.baseurl }}/assets/images/ai-for-testing/how-ai-chatgpt-generate-test-data-write-auto-performance-test/Untitled 1.png)

# Inquire Chatgpt to write automation test script to generate test data automatically

This script defines functions to generate random usernames, passwords, phone numbers, and addresses for users. Then, it generates user data for the desired number of users, writes it to a JSON file named `users_data.json`, and prints a confirmation message.

![walking]({{ site.baseurl }}/assets/images/ai-for-testing/how-ai-chatgpt-generate-test-data-write-auto-performance-test/Untitled 2.png)

Here is the test script that Chatgpt returned:

```python
import json
import random
import string

def generate_username(first_name, last_name):
    return first_name.lower() + last_name.lower() + str(random.randint(10, 99))

def generate_password():
    characters = string.ascii_letters + string.digits + string.punctuation
    return ''.join(random.choices(characters, k=12))

def generate_phone():
    return f"({random.randint(100, 999)}) {random.randint(100, 999)}-{random.randint(1000, 9999)}"

def generate_address():
    streets = ["Oak", "Pine", "Maple", "Elm", "Birch", "Willow", "Cedar", "Walnut", "Magnolia"]
    cities = ["Springfield", "Lakeside", "Rivertown", "Hilltop", "Harborview", "Sunnyvale", "Oceanview", "Riverside", "Lakeshore", "Hillside", "Greenfield", "Meadowview", "Hillcrest", "Lakewood", "Oakwood", "Riverdale", "Mountainview"]
    return f"{random.randint(100, 999)} {random.choice(streets)} Street, {random.choice(cities)}, USA"

def generate_users(num_users):
    users = []
    for _ in range(num_users):
        first_name = random.choice(["Alex", "Sarah", "Mike", "Laura", "Chris", "Jenny", "Kevin", "Emily", "David", "Jessica", "Matt", "Rachel", "Ryan", "Amanda", "Brian", "Jessie", "Justin", "Katie", "Steven", "Olivia"])
        last_name = random.choice(["Jones", "Miller", "Peters", "Smith", "Wilson", "Brown", "Baker", "Jones", "Clark", "Lee", "Adams", "Smith", "Davis", "Rodriguez", "Hernandez", "Evans", "Parker", "Morris", "Richards", "Jenkins"])
        username = generate_username(first_name, last_name)
        password = generate_password()
        phone = generate_phone()
        address = generate_address()
        user = {
            "username": username,
            "password": password,
            "first_name": first_name,
            "last_name": last_name,
            "phone": phone,
            "address": address
        }
        users.append(user)
    return users

def write_to_json_file(data, filename):
    with open(filename, 'w') as f:
        json.dump(data, f, indent=4)

if __name__ == "__main__":
    num_users = 20
    users_data = generate_users(num_users)
    filename = "users_data.json"
    write_to_json_file(users_data, filename)
    print(f"{num_users} users' data has been generated and saved to {filename}.")

```

# Inquiring ChatGPT to write Python performance test script with Locust

![walking]({{ site.baseurl }}/assets/images/ai-for-testing/how-ai-chatgpt-generate-test-data-write-auto-performance-test/Untitled 3.png)

```python
import random
from locust import HttpUser, between, task

class SignupUser(HttpUser):
    wait_time = between(5, 9)

    def generate_username(self):
        return ''.join(random.choices('abcdefghijklmnopqrstuvwxyz', k=5))

    def generate_password(self):
        return ''.join(random.choices('abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789!@#$%^&*()', k=12))

    def generate_first_name(self):
        return random.choice(["John", "Jane", "Michael", "Emily", "David", "Sarah", "Chris", "Emma", "Matthew", "Olivia"])

    def generate_last_name(self):
        return random.choice(["Smith", "Johnson", "Williams", "Jones", "Brown", "Davis", "Miller", "Wilson", "Moore", "Taylor"])

    def generate_phone(self):
        return f"{random.randint(100, 999)}-{random.randint(100, 999)}-{random.randint(1000, 9999)}"

    def generate_address(self):
        return f"{random.randint(100, 999)} {random.choice(['Main', 'Elm', 'Oak', 'Maple', 'Cedar', 'Pine'])} St, Anytown, USA"

    @task
    def sign_up(self):
        username = self.generate_username()
        password = self.generate_password()
        first_name = self.generate_first_name()
        last_name = self.generate_last_name()
        phone = self.generate_phone()
        address = self.generate_address()
        
        data = {
            "username": username,
            "password": password,
            "first_name": first_name,
            "last_name": last_name,
            "phone": phone,
            "address": address
        }

        self.client.post("/sign-up", json=data, name="/sign-up")

```

In this script:

- We import necessary modules from Locust.
- We define a `SignupUser` class that inherits from `HttpUser`.
- We define methods to generate random values for username, password, first name, last name, phone, and address.
- We define a `sign_up` task that generates user data and makes a POST request to `/sign-up` endpoint with that data.
- The `wait_time` attribute specifies a range for the time that a simulated user will wait between executing tasks.

You can run this Locust script using the Locust command line interface (CLI) with appropriate parameters such as number of users and hatch rate. For example:

```powershell
locust -f locust_signup.py --headless -u 50 -r 10
```

This will simulate 50 users with a hatch rate of 10 users per second executing the `sign_up` task defined in the script. Adjust the parameters according to your testing needs.