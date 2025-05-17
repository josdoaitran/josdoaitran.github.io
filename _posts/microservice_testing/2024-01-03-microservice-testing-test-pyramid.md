---
layout: post
title:  "Key points about Microservice Testing - Test Pyramid - QA should aware ?"
author: donald
categories: [ microservice-test, collection, event-driven ]
image: assets/images/microservice-testing/monolithic-vs-microservices-architecture.png
tags: [tutorial, microservice-test, event-driven]
---

In some cases, there are many guys as QA, Tester who don't have much knowledge and awareness in some complex technical point or who interested in how SUT (System Under Test) work. It becomes a big challenges in exploring and doing testing better.

# What is Microservice vs Monolithic - System Architecture?
 
In software development, there are two main architectural approaches: Monolithic and Microservices. Understanding these architectures is crucial for making informed decisions about system design and testing strategies.

## Monolithic Architecture

A monolithic application is built as a single, unified unit where all components are interconnected and interdependent.

### Characteristics:
- All components are tightly coupled
- Single codebase
- Single deployment unit
- Shared database
- All functionality runs in the same process

### Advantages:
- Simpler to develop initially
- Easier to debug and test (everything is in one place)
- Straightforward deployment (single unit)
- Better performance for simple applications
- Lower operational complexity

### Disadvantages:
- Limited scalability (must scale the entire application)
- Difficult to maintain as the application grows
- Technology stack is locked in
- Single point of failure
- Longer build and deployment times
- Harder to adopt new technologies

### Choose Monolithic When:
- Building a small to medium-sized application
- Team size is small
- Application has simple business logic
- Quick time-to-market is crucial
- Limited resources for infrastructure

## Microservice Architecture

Microservices architecture breaks down an application into a collection of small, independent services that communicate with each other.

### Characteristics:
- Services are loosely coupled
- Each service has its own codebase
- Independent deployment
- Each service can have its own database
- Services communicate via APIs or message queues
- Each service runs in its own process

### Advantages:
- Better scalability (services can be scaled independently)
- Easier to maintain and update
- Technology diversity (each service can use different technologies)
- Fault isolation
- Faster deployment cycles
- Better alignment with business capabilities
- Easier to understand and modify individual services

### Disadvantages:
- More complex to develop and test
- Requires more infrastructure and operational overhead
- Network latency between services
- More challenging to maintain data consistency
- Requires more sophisticated monitoring and logging
- Higher initial development time

### Choose Microservices When:
- Building a large, complex application
- Need to scale specific parts of the application
- Team is large and can be split into smaller teams
- Different parts of the application have different scaling needs
- Need to use different technologies for different services
- Application needs to be highly available and fault-tolerant


## Key Differences

![walking]({{ site.baseurl }}/assets/images/microservice-testing/monolithic-vs-microservices-architecture.png)
*Figure 1: Visual comparison of Monolithic and Microservices architectures*

| Aspect | Monolithic | Microservices |
|--------|------------|---------------|
| **Size** | Large, single unit | Small, independent services |
| **Coupling** | Tightly coupled | Loosely coupled |
| **Deployment** | Single deployment | Independent deployments |
| **Scaling** | Scale entire application | Scale individual services |
| **Database** | Single shared database | Multiple databases possible |
| **Technology** | Single technology stack | Multiple technology stacks possible |
| **Development** | Simpler initial development | More complex initial setup |
| **Maintenance** | Harder as application grows | Easier to maintain individual services |
| **Testing** | Simpler to test | More complex testing requirements |
| **Performance** | Better for simple applications | Better for complex, scalable applications |

Understanding these architectural differences is crucial for implementing appropriate testing strategies, which we'll explore in the following sections about the test pyramid and testing approaches.

```
┌───────────────────────────────────────────────────────────┐   ┌───────────────────────────────────────┐
│                   MONOLITHIC ARCHITECTURE                 │   │      MICROSERVICES ARCHITECTURE       │
├───────────────────────────────────────────────────────────┤   ├───────────────────────────────────────┤
│                                                           │   │    ┌─────────────┐  ┌─────────────┐   │
│  ┌─────────────┐                                          │   │    │  User API   │  │   Product   │   │
│  │             │                                          │   │    │   Service   │  │   Service   │   │
│  │    User     │                                          │   │    └──────┬──────┘  └──────┬──────┘   │
│  │  Interface  │                                          │   │           │                │          │
│  │             ├─────────────────────────┐                │   │           │                │          │
│  └─────────────┘                         │                │   │    ┌──────▼──────┐  ┌──────▼──────┐   │
│                                          │                │   │    │    Order    │  │  Inventor   │   │
│                                          │                │   │    │   Service   │  │   Service   │   │
│  ┌─────────────┐  ┌─────────────┐  ┌─────▼─────┐          │   │    └──────┬──────┘  └──────┬──────┘   │
│  │             │  │             │  │           │          │   │           │                │          │
│  │   User      │  │   Product   │  │  Order    │          │   │    ┌──────▼──────┐  ┌──────▼──────┐   │
│  │  Management │  │  Catalog    │  │ Processing│          │   │    │   Payment   │  │   Shipping  │   │
│  │             │  │             │  │           │          │   │    │   Service   │  │   Service   │   │
│  └─────────────┘  └─────────────┘  └───────────┘          │   │    └─────────────┘  └─────────────┘   │
│                                                           │   │                                       │
│                                                           │   │    ┌─────────────────────────────┐    │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐        │   │    │                             │    │
│  │             │  │             │  │             │        │   │    │     Message Broker/Bus      │    │
│  │  Inventory  │  │   Payment   │  │  Shipping   │        │   │    │   (Kafka/RabbitMQ/etc.)     │    │
│  │  Management │  │  Processing │  │  Management │        │   │    │                             │    │
│  │             │  │             │  │             │        │   │    └─────────────────────────────┘    │
│  └─────────────┘  └─────────────┘  └─────────────┘        │   │                                       │
│                                                           │   │                                       │
│  ┌───────────────────────────────────────────────┐        │   │                                       │
│  │                                               │        │   │                                       │
│  │             Single Shared Database            │        │   │                                       │
│  │                                               │        │   │                                       │
│  └───────────────────────────────────────────────┘        │   │    ┌─────┐  ┌─────┐  ┌─────┐  ┌─────┐ │
│                                                           │   │    │ DB  │  │ DB  │  │ DB  │  │ DB  │ │
└───────────────────────────────────────────────────────────┘   │    └─────┘  └─────┘  └─────┘  └─────┘ │
                                                                └───────────────────────────────────────┘

┌───────────────────────────────────────────────┐   ┌───────────────────────────────────────────────┐
│          MONOLITHIC CHARACTERISTICS           │   │         MICROSERVICES CHARACTERISTICS         │
├───────────────────────────────────────────────┤   ├───────────────────────────────────────────────┤
│ • Single deployable unit                      │   │ • Multiple independently deployable services  │
│ • Shared codebase                             │   │ • Separated codebases                         │
│ • Single database                             │   │ • Database per service                        │
│ • Tightly coupled components                  │   │ • Loosely coupled services                    │
│ • Typically one programming language          │   │ • Polyglot programming (multiple languages)   │
│ • Scaled as a complete unit                   │   │ • Independent scaling per service             │
│ • Simpler to develop initially                │   │ • More complex initial setup                  │
│ • Harder to maintain as it grows              │   │ • Easier to maintain individual services      │
│ • Single point of failure                     │   │ • Resilient to partial system failures        │
│ • Slower deployment pipeline                  │   │ • Faster, independent deployment cycles       │
└───────────────────────────────────────────────┘   └───────────────────────────────────────────────┘
```

# Understanding the Test Pyramid in Microservice Testing

The Test Pyramid is a fundamental concept in software testing that helps teams maintain a balanced testing strategy. In the context of microservices, understanding and implementing the test pyramid becomes even more crucial due to the distributed nature of the system.

## Essential Test Types in the Test Pyramid



### 1. Unit Tests (Base Layer)
- **Purpose**: Test individual units of code in isolation
- **Scope**: 
  - Individual functions/methods
  - Smallest testable parts
  - Business logic within a service
- **Key Characteristics**:
  - Fastest execution
  - Highest number of tests
  - No external dependencies
  - Use of mocks/stubs
- **Example**: Testing a service's business logic methods
- **Tools**: JUnit, NUnit, PyTest, Jest

### 2. Component Tests (Service Level)
- **Purpose**: Test individual microservices in isolation
- **Scope**:
  - Entire service functionality
  - Service's internal components
  - Service's database interactions
- **Key Characteristics**:
  - Test service as a black box
  - Mock external service dependencies
  - Include service's database
  - Test service's API endpoints
- **Example**: Testing a User Service's complete functionality
- **Tools**: Spring Boot Test, TestContainers

### 3. Contract Tests (Integration Level)
- **Purpose**: Verify service interfaces and interactions
- **Scope**:
  - Service-to-service communication
  - API contracts
  - Message formats
  - Data schemas
- **Key Characteristics**:
  - Verify producer-consumer contracts
  - Ensure backward compatibility
  - Test API specifications
  - Validate message formats
- **Example**: Testing API contracts between Order and Payment services
- **Tools**: Pact, Spring Cloud Contract

### 4. End-to-End Tests (System Level)
- **Purpose**: Test complete business flows across services
- **Scope**:
  - Complete user journeys
  - Cross-service workflows
  - System integration
  - Business processes
- **Key Characteristics**:
  - Slowest execution
  - Fewest number of tests
  - Test real service interactions
  - Verify business requirements
- **Example**: Testing complete order-to-delivery flow
- **Tools**: Selenium, Cypress, Karate

### 5. Exploratory Testing (Complementary)
- **Purpose**: Discover unknown issues and validate user experience
- **Scope**:
  - System behavior
  - User experience
  - Edge cases
  - Unforeseen scenarios
- **Key Characteristics**:
  - Manual testing approach
  - Unscripted testing
  - Real user scenarios
  - Creative test scenarios
- **When to Use**:
  - New feature validation
  - Complex user flows
  - Usability testing
  - Security testing
  - Performance investigation
- **Tools**: Session-based testing, Mind maps, Test charters

## Test Distribution Guidelines

1. **Unit Tests (60-70%)**
   - Highest number of tests
   - Fast execution
   - High coverage of business logic
   - Easy to maintain

2. **Component Tests (15-20%)**
   - Test service boundaries
   - Verify service functionality
   - Include database tests
   - Mock external dependencies

3. **Contract Tests (10-15%)**
   - Verify service interfaces
   - Ensure API compatibility
   - Test message contracts
   - Validate data schemas

4. **E2E Tests (5-10%)**
   - Critical business paths
   - Key user journeys
   - System integration
   - Cross-service workflows

5. **Exploratory Testing (As needed)**
   - Not part of the pyramid
   - Complementary to automated tests
   - Focus on user experience
   - Discover unknown issues

## Best Practices for Each Test Type

### Unit Tests
- Keep tests focused and small
- Use meaningful test names
- Follow AAA pattern (Arrange, Act, Assert)
- Mock external dependencies
- Maintain high coverage of business logic

### Component Tests
- Test service as a whole
- Use test databases
- Mock external services
- Test error scenarios
- Verify service configuration

### Contract Tests
- Maintain backward compatibility
- Version your contracts
- Test both positive and negative scenarios
- Include schema validation
- Document API changes

### E2E Tests
- Focus on critical paths
- Keep tests independent
- Use realistic test data
- Handle asynchronous operations
- Implement proper cleanup

### Exploratory Testing
- Create test charters
- Document findings
- Focus on user experience
- Test edge cases
- Validate non-functional requirements

## Common Challenges and Solutions

1. **Test Data Management**
   - Use test databases
   - Implement data cleanup
   - Create test data factories
   - Use data versioning

2. **Test Environment**
   - Use containerization
   - Implement service virtualization
   - Maintain environment parity
   - Automate environment setup

3. **Test Maintenance**
   - Regular test reviews
   - Update test documentation
   - Refactor test code
   - Monitor test stability

4. **Test Execution**
   - Parallel test execution
   - Optimize test suites
   - Implement test prioritization
   - Use test reporting tools

By following these guidelines and maintaining a balanced test pyramid, teams can ensure comprehensive test coverage while maintaining efficient test execution and maintenance.

# Why Microservice Testing is Essential

In today's modern software architecture, microservices have become a popular approach for building scalable and maintainable applications. However, with this architectural style comes unique challenges that make comprehensive testing absolutely crucial. Here's why microservice testing is a must:

## 1. Distributed System Complexity
- Microservices operate as independent, distributed systems
- Each service can be developed, deployed, and scaled independently
- Services communicate through APIs, message queues, or event streams
- This distributed nature increases the complexity of testing as you need to verify both individual service behavior and their interactions.
This point will be demonstrated again in Test Pyramid to have the full testing types and testing levels in cover testing both individual service, communication among them and how entire software works.

## 2. Independent Deployment Risks
- Services can be deployed independently
- Changes in one service might affect others without immediate visibility
- Testing helps catch integration issues before they reach production
- Ensures backward compatibility when services are updated

## 3. Data Consistency Challenges
- Each microservice might have its own database
- Data consistency across services needs to be verified
- Testing helps ensure data integrity across service boundaries
- Validates that distributed transactions work as expected.
Data Consistency will be a part of our checklist or test cases in higher levels of testing. Especially, When we perform e2e testing when all microservices integrated and work together.

## 4. Performance and Scalability
- Services need to handle varying loads independently
- Performance bottlenecks in one service can affect the entire system
- Testing helps identify scalability issues early
- Ensures the system can handle expected and peak loads.
Besides functional Testing, the non-functional testing for microservice could be a big challenges.

When we have 2 main views:
- Performance testing for each microservice: where we consider the availability of each microservice in a specify workload.
- Performance testing for entire software as e2e performance testing: we have to determine the capacity, availability, realibility of entire software when they serve the full business flow under specify workload.

## 5. Fault Tolerance and Resilience
- Services must be resilient to failures in other services
- Testing helps verify fallback mechanisms and circuit breakers
- Ensures graceful degradation when dependencies fail
- Validates that the system can recover from failures

## 6. Security Concerns
- More services mean more potential security vulnerabilities
- Each service needs to be tested for security
- API endpoints need to be verified for proper authentication and authorization
- Testing helps identify security gaps in service interactions

## 7. Contract Testing
- Services communicate through well-defined contracts
- Changes in one service's API can break dependent services
- Contract testing ensures API compatibility
- Helps maintain backward compatibility

## 8. End-to-End Business Flows
- Business processes often span multiple services
- Testing ensures that business workflows function correctly
- Validates that the system meets business requirements
- Helps maintain business continuity

By implementing a comprehensive testing strategy for microservices, organizations can:
- Reduce the risk of production failures
- Improve system reliability
- Maintain service quality
- Enable faster and safer deployments
- Build confidence in the system's behavior

# Refferences and Modern Test Pyramid
Most of above knowledge are collected from many resources as bellow:
- [Martinfowler Test Microservice](https://martinfowler.com/articles/practical-test-pyramid.html)
- [Headspin Testing Pyramid](https://www.headspin.io/blog/the-testing-pyramid-simplified-for-one-and-all)
- [Contract Testing vs Integration testing - Pactflow](https://pactflow.io/blog/contract-testing-vs-integration-testing/)

However !! Exciting with Modern Test Pyramind, how we can optimize and accelarate testing more effectively.
## HoneyComb Test Model:
You can refer more via: 
- [HoneyComb Test Model ss-tech](https://medium.com/@ss-tech/the-honeycomb-test-model-a-holistic-approach-to-software-testing-a9dd39475ee9)
- [HoneyComb Spootyfy - Test Microservice]https://engineering.atspotify.com/2018/01/testing-of-microservices)
## Modern Test Pyramid
We expanded more types of testing and levels of testing, we should arrange them effectively also to optimize them.
reffer to these link:
- [Modern-test-pyramid](https://dev.to/optivem/modern-test-pyramid-4dfc)
- [New Test Pyramid - Valentina](https://journal.optivem.com/p/new-test-pyramid)

![walking]({{ site.baseurl }}/assets/images/microservice-testing/modern-test-pyramid.png)
