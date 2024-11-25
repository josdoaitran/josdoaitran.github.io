---
layout: post
title:  "Performance test - Different views between Client Side and Server/Service Side"
author: donald
categories: [ Testing4Everyone, tutorial ]
image: assets/images/performance-testing/performance-test-client-view-server-view.png
---
In Web application and Mobile application, The view of Client Side and Server Side discribes the overview how our application works in the Internet views. In Client-Server view, the EndUser will use FrontEnd app to communicate with Backend app via the Internet connection base.

End user devices such as laptops, smartphones, and desktop computers are considered to be 'clients' of the servers, as if they were customers obtaining services from a company. Client devices send requests to the servers for webpages or applications, and the servers serve up responses.

![](assets/images/performance-testing/performance-test-client-view-server-view.png)

**Client Side**: In Web application and Mobile application, Client View are what we see in UI, takes places on client (Browser or Mobile application).

This includes: text, images, and the rest of the UI, along with any actions that an application performs within the user's browser / mobile app. (Web app: Markup languages like HTML and CSS are interpreted by the browser on the client side).

**Server Side**: Server Side means everything that happens on the server, instead of on the client. It includes: Load Balancer, Business Services (Container on micro-service view), Database, Server base with Infrastructure view, ...

All actions from End-Users do on their browsers or mobile application will be transferred as requests to Server sides to request functions of the application provides. Once the requests come to Server, the server with components will handle to do what client side expect before return or response the correct responses.

![](assets/images/performance-testing/client-view-vs-server-view.png)

**References:**
- Client Side, Server Side: https://www.cloudflare.com/learning/serverless/glossary/client-side-vs-server-side/