---
layout: post
title:  "AI write script - Performance Test with Locust"
author: donald
categories: [ ai-test, ai-agent, llm, mcp-ai ]
image: assets/images/ai-for-testing/how-ai-chatgpt-write-test-script-performance-test-locust/Untitled 2.png
tags: [tutorial, ai-for-testing]
---
Use AI (Chatgpt) to write test script in Data Driven in Performance test

# Overview

In order to help us understanding the ways that I am taking advantages of powerful capabilities of AI (ChatGPT) to boost my productivities. Although, I have to validate all suggestions from ChatGPT, how to make sure whether it is useful or not (**Accuracy and Testing Mindset**).

Scenarios in this post: I have a simple service (Allows End-User login from Username and Password, then they can get the list of new feeds from Backend).

**I expect that I can write quickly the performance test script with the list of users saved in a JSON file**

Here is the full of pictures I already worked with ChatGPT.

I requested ChatGPT help me write a test script for performance test in **Locust** from a CURL ass below:

```powershell
curl --location 'http://127.0.0.1:5000/login' \
--header 'Content-Type: application/json' \
--data '{
  "username": "admin",
  "password": "admin123"
}'
```

And here is the list of users, I have in my example system

```powershell
[
    {
        "username": "admin",
        "password": "admin123"
    },
    {
        "username": "john.doe",
        "password": "JohnsPassword1"
    },
    {
        "username": "jane.smith",
        "password": "Jane1234!"
    },
    {
        "username": "alice.wonder",
        "password": "Wonderland@5"
    },
    {
        "username": "bob.builder",
        "password": "CanWeFixIt$2"
    },
    {
        "username": "charlie.brown",
        "password": "Peanuts123"
    }   
]
```

After I login with the valid credentials, I will received the token, and use it to get the list of feeds in the API request as CURL information as below:

```powershell
curl --location 'http://127.0.0.1:5000/feed' \
--header 'token: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImFkbWluIn0.vb1PIGc2ZoxpcJ0sPAYCjc4-D1o3nCzCyNZiWWYZy3E'
```

# 1 - Write a Locust Python script with Chatgpt

Firstly, I asked Chatgpt AI to help me write a Locust python script to test Login

```powershell
Hey, Could you help me write a Locust python script to test login api as curl information ?
curl --location 'http://127.0.0.1:5000/login' \
--header 'Content-Type: application/json' \
--data '{
  "username": "admin",
  "password": "admin123"
}'
```

Here is the response from Chatgpt

![walking]({{ site.baseurl }}/assets/images/ai-for-testing/how-ai-chatgpt-write-test-script-performance-test-locust/Untitled.png)

Here is the locust script content that Chatgpt returned:

```powershell
from locust import HttpUser, TaskSet, task, between

class LoginTaskSet(TaskSet):
    @task
    def login(self):
        self.client.post("/login", json={"username": "admin", "password": "admin123"})

class WebsiteUser(HttpUser):
    tasks = [LoginTaskSet]
    wait_time = between(1, 5)  # Wait time between tasks

if __name__ == "__main__":
    import os
    os.system("locust")

```

We also follow the steps to save the script as file: **locustfile.py**

![walking]({{ site.baseurl }}/assets/images/ai-for-testing/how-ai-chatgpt-write-test-script-performance-test-locust/Untitled 1.png)

**I already validate again, to make sure the test script work correctly 🙂 (Test the test script ⇒ validation and Accuracy mindset)**

![walking]({{ site.baseurl }}/assets/images/ai-for-testing/how-ai-chatgpt-write-test-script-performance-test-locust/Untitled 2.png)

And here is the result on Locust report:

![walking]({{ site.baseurl }}/assets/images/ai-for-testing/how-ai-chatgpt-write-test-script-performance-test-locust/Untitled 3.png)

And log of server (System-under-Test):

![walking]({{ site.baseurl }}/assets/images/ai-for-testing/how-ai-chatgpt-write-test-script-performance-test-locust/Untitled 4.png)

It is proved that, the example script from Chatgpt is working well.

# 2 - Request Chatgpt a test script reading data from JSON file

However, it still need to be updated more, how it allows us generate requests with dynamic data of users login. Therefore, I requested Chatgpt update the test script, how we can read data from a JSON file, where we saved all users data for performance testing as bellow

```powershell
[
    {
        "username": "admin",
        "password": "admin123"
    },
    {
        "username": "john.doe",
        "password": "JohnsPassword1"
    },
    {
        "username": "jane.smith",
        "password": "Jane1234!"
    },
    {
        "username": "alice.wonder",
        "password": "Wonderland@5"
    },
    {
        "username": "bob.builder",
        "password": "CanWeFixIt$2"
    },
    {
        "username": "charlie.brown",
        "password": "Peanuts123"
    }   
]
```

I raised the request as below:

![walking]({{ site.baseurl }}/assets/images/ai-for-testing/how-ai-chatgpt-write-test-script-performance-test-locust/Untitled 5.png)

And Chatgpt responded to me as below:

- it suggested me to save all data as a JSON file

![walking]({{ site.baseurl }}/assets/images/ai-for-testing/how-ai-chatgpt-write-test-script-performance-test-locust/Untitled 6.png)

Modify the test script as below:

![walking]({{ site.baseurl }}/assets/images/ai-for-testing/how-ai-chatgpt-write-test-script-performance-test-locust/Untitled 7.png)

Here is the content of modified script:

```powershell
import json
import random
from locust import HttpUser, TaskSet, task, between

# Load user data from JSON file
with open('users.json', 'r') as file:
    users = json.load(file)

class LoginTaskSet(TaskSet):
    @task
    def login(self):
        # Select a random user from the list
        user = random.choice(users)
        username = user['username']
        password = user['password']
        
        # Perform login request
        self.client.post("/login", json={"username": username, "password": password})

class WebsiteUser(HttpUser):
    tasks = [LoginTaskSet]
    wait_time = between(1, 5)  # Wait time between tasks

if __name__ == "__main__":
    import os
    os.system("locust")

```

We run again with this configuration:

![walking]({{ site.baseurl }}/assets/images/ai-for-testing/how-ai-chatgpt-write-test-script-performance-test-locust/Untitled 8.png)

Here is the result on Locust report

![walking]({{ site.baseurl }}/assets/images/ai-for-testing/how-ai-chatgpt-write-test-script-performance-test-locust/Untitled 9.png)

and log response on service

![walking]({{ site.baseurl }}/assets/images/ai-for-testing/how-ai-chatgpt-write-test-script-performance-test-locust/Untitled 10.png)

**In conclusion, we refer to supports from ChatGPT only, we should NOT depend on and NOT trust in  all information completely. As above information and steps I did, we have to modify and test all information that Chatgpt suggested us.**