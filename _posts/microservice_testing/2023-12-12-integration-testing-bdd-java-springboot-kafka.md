---
layout: post
title:  "Integration Testing - BDD - Java Springboot - Kafka Embedded - Mysql - Tutorial"
author: donald
categories: [ microservice-test, collection, event-driven ]
image: assets/images/microservice-testing/monolithic-vs-microservices-architecture.png
tags: [tutorial, microservice-test, event-driven]
---

# Integration Testing - BDD - Java Springboot - Kafka Embedded - Mysql - Tutorial

Owner: josdoaitran
Verification: Verified

In this post, I would like share with us the examples of automated testing for covering several testing levels for system working in Micro-service model.

Before we research automated testing for Kafka Micro-service, we need to have the example micro-services, they transfers the information through Kafka - Event Message.

In the example, I build the basic feature: sign-up the new user and get user status.

We will have 2 Java SpringBoot services with Mysql: User-Service and Fraud-Check-Service.

**Example Micro-service with Kafka and Event-Streaming**
![walking]({{ site.baseurl }}/assets/images/microservice-testing/integration-testing-bdd-java-springboot-kafka/Untitled.png)

The business context of example micro-services with Kafka.

- As a new client, he/she can sign-up a new account in system by username and phone number.

User-Service expose the API and enable client to make POST **/user/sign-up** request.

+ URL: **/user/sign-up**

+ Method: **POST**

+ Request Body:

```json
{
    "name":"Testing1",
    "phone":"0908917484"
}
```

After User-Service receive the request message, they will process to create a new user in Service or not.

If yes, User-Service will produce a message to **CREATE_NEW_USER_TOPIC** topic.

Then, Fraud-Check-Service will consume the message and process the checking rules to make a decision to change the status of new user to **BLOCKED** or **PENDING**.

In the next process, Fraud-Check-Service will push a new message to **UPDATE_USER_STATUS_TOPIC** topic to update the new status for User-Service

- As a client, he/she can get information of user in system.

User-Service expose the API to enable client to get the lasted his/ her status and account info on User-Service.

+ URL: **/user/get-userinfo/{phone}**

+ Method: **GET**

**About Kafka - Event Driven**

![walking]({{ site.baseurl }}/assets/images/microservice-testing/integration-testing-bdd-java-springboot-kafka/Untitled 1.png)

In this post, I don't mention and explain about Kafka and Event Streaming system. If you need to explore more about Kafka and Event-Streaming system, you can refer more information about Kafka:
[https://kafka.apache.org/](https://kafka.apache.org/).

## Acceptance Test Cases

In order to cover testing for these business rule, probably there are many testing levels we should cover.

And In this post I would like to focus on Integration test / Component test level and give us the example approaches to cover automated testing for Kafka-Event Streaming micro-service.

Now, I would like to mention some essential test cases in this post to help us cover the Acceptance Criteria for my Business Context of example features with Kafka-Event Streaming micro-service.

We cover some cases for User-Service.

![walking]({{ site.baseurl }}/assets/images/microservice-testing/integration-testing-bdd-java-springboot-kafka/Untitled 2.png)

We can apply Black-Box testing-technique to define above test cases to assure User-Service meet my business context.

Integration testing for our micro-services bring us a lot of value such as:

- isolate dependencies
- earlier testing
- faster testing
- easy-to-test more cases.

**Java SpringBoot - Integration Testing - Kafka Embedded - H2 Database library**

![walking]({{ site.baseurl }}/assets/images/microservice-testing/integration-testing-bdd-java-springboot-kafka/Untitled 3.png)

### h2 dependency:

h2 dependency is used to replace for the real database, in our testing in Integration testing and UnitTest as well.

Define h2 dependency in POM:

```xml
<dependency>
   <groupId>com.h2database</groupId>
   <artifactId>h2</artifactId>
   <version>1.4.194</version>
</dependency>
```

### Kafka Embedded dependency:

With the same approach and target, we use Kafka Embedded to replace our real Kafka Server in Test Environment.

Kafka Embedded library are mentioned and defined in **spring-kafka-test**

then, we define spring-kafka-test dependency in POM:

```xml
<dependency>
   <groupId>org.springframework.kafka</groupId>
   <artifactId>spring-kafka-test</artifactId>
   <version>${spring-kafka.version}</version>
   <scope>test</scope>
</dependency>
```

**Java Springboot test configuration**

```prolog
################ Configuration Mock Database h2 ##################################
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
logging.level.org.springframework.web: DEBUG
jdbc.driverClassName=org.h2.Driver
jdbc.url=jdbc:h2:mem:myDb;DB_CLOSE_DELAY=-1

hibernate.dialect=org.hibernate.dialect.H2Dialect
hibernate.hbm2ddl.auto=create

################ Configuration Microservice  ###############################################
server.port=8081

################ Configuration Kafka  ######################################################
#spring.kafka.bootstrap-servers=localhost:9092
spring.kafka.bootstrap-servers=${spring.embedded.kafka.brokers}
spring.kafka.producer.key-serializer=org.apache.kafka.common.serialization.StringSerializer
spring.kafka.producer.value-serializer=org.springframework.kafka.support.serializer.JsonSerializer
#spring.kafka.producer.properties.spring.json.add.type.headers=false

spring.kafka.consumer.bootstrap-servers=${spring.embedded.kafka.brokers}
spring.kafka.consumer.group-id=group_id
spring.kafka.consumer.auto-offset-reset=earliest
spring.kafka.consumer.key-deserializer=org.apache.kafka.common.serialization.StringDeserializer
spring.kafka.consumer.value-deserializer=org.springframework.kafka.support.serializer.JsonDeserializer
spring.kafka.consumer.properties.spring.json.trusted.packages=*
```

In this SpringBoot test, I integrate our test with BDD Cucumber, then we need to add Java-Springboot-Test-Kafka and SpringBoot-Cucumber as below:

```xml
<dependency>
   <groupId>io.cucumber</groupId>
   <artifactId>cucumber-java</artifactId>
   <version>${cucumber.version}</version>
   <scope>test</scope>
</dependency>
<dependency>
   <groupId>io.cucumber</groupId>
   <artifactId>cucumber-spring</artifactId>
   <version>${cucumber.version}</version>
   <scope>test</scope>
</dependency>
<dependency>
   <groupId>io.cucumber</groupId>
   <artifactId>cucumber-junit</artifactId>
   <version>${cucumber.version}</version>
   <scope>test</scope>
</dependency>
```

In order to enable Kafka-Embedded and h2 database, we will initialize the configure on Java-Spring-Test Class, our StepDefinition will be extended Java-Spring-Test Class.

- Base SpringTest class

```java
import com.testing4everyone.kafka.user.service.UserServiceApplication;
import io.cucumber.spring.CucumberContextConfiguration;
import org.junit.jupiter.api.Tag;
import org.junit.jupiter.api.extension.ExtendWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.kafka.test.context.EmbeddedKafka;
import org.springframework.test.context.ActiveProfiles;
import org.springframework.test.context.junit.jupiter.SpringExtension;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;

@ExtendWith(SpringExtension.class)
@CucumberContextConfiguration
@SpringBootTest(classes = {UserServiceApplication.class}, webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
@ActiveProfiles({"kafka-embedded"})
@Tag("AcceptanceTest")
@AutoConfigureMockMvc
@EmbeddedKafka(partitions = 1, topics = {"CREATE_NEW_USER_TOPIC", "UPDATE_USER_INFO_TOPIC"}, controlledShutdown = true,
    brokerProperties = {"log.dir=build/tmp/kafka-data/${spring.application.name}"})
public class SpringAcceptanceTest {
    @Autowired
    protected MockMvc mockMvc;
}
```

StepDefinition Class:

```java
public class TestDefs extends SpringAcceptanceTest {
    private static final Logger logger = LoggerFactory.getLogger(TestDefs.class);

    @Autowired
    private ObjectMapper objectMapper;

    @Autowired
    UserRepository userRepository;

    @Autowired
    private EmbeddedKafkaBroker embeddedKafkaBroker;

    @Given("^Clear User information in User Service by Phone = (.*)$")
    public void initTestData(String phone) {
        try{
            userRepository.deleteById(userRepository.findByPhone(phone).getId());
        }catch (Exception e){
            logger.info("No reset");
        }
    }

    @Given("^UserID = (.*) has Name = (.*) Phone = (.*) and Status = (.*) in User Service$")
    public void userInfoInSignupService(int id, String name, String phone, String status) {
        User prepareUser = new User();
        prepareUser.setId(id);
        prepareUser.setName(name);
        prepareUser.setPhone(phone);
        prepareUser.setStatus(status);
        userRepository.save(prepareUser);
    }

    private MvcResult mvcResult;

    @When("^Request to get User information by Phone = (.*)$")
    public void getUserInformationByPhone(String phone) throws Exception {
        mvcResult = mockMvc.perform(get("/user/get_userid/" + phone)
                        .contentType(MediaType.APPLICATION_JSON))
                .andDo(print())
                .andExpect(status().is2xxSuccessful())
                .andReturn();
    }

    @Then("^TestCase (.*): I expect API get User by Phone = (.*) will return Name = (.*) and Status = (.*)$")
    public void testcaseGetUserIdReturnResult(int testCaseNo, String phone, String name, String userStatus) throws Exception {
        User userResponse = objectMapper.readValue(mvcResult.getResponse().getContentAsString(), User.class);
        assertThat(userResponse);
        userStatus.replace(" ","");
        userResponse.getStatus();
        assertThat(userStatus.replace(" ","")).isEqualTo(userResponse.getStatus());
        assertThat(name).isEqualTo(userResponse.getName());
        assertThat(phone).isEqualTo(userResponse.getPhone());
    }

    @Then("^TestCase (.*): I expect response message contain Phone = (.*) Name = (.*) Status = (.*)$")
    public void testPublishEmployee(String testcase, String phone, String name, String userStatus) throws IOException, InterruptedException, ExecutionException {
        User signUpUserResponse = objectMapper.readValue(mvcResult.getResponse().getContentAsString(), User.class);

        assertThat(signUpUserResponse);
        assertThat(userStatus.replace(" ","")).isEqualTo(signUpUserResponse.getStatus());
        assertThat(name).isEqualTo(signUpUserResponse.getName());
        assertThat(phone).isEqualTo(signUpUserResponse.getPhone());

    }

    private Consumer<String, User> consumerServiceTest;

    @Given("^Prepare consumer listen Topic = (.*)$")
    public void prepareConsumer(String topic){
        Map<String, Object> consumerProps = KafkaTestUtils.consumerProps("group_json", "false", embeddedKafkaBroker);
        consumerProps.put(ConsumerConfig.AUTO_OFFSET_RESET_CONFIG, "earliest");
        ConsumerFactory cf = new DefaultKafkaConsumerFactory<String, User>(consumerProps, new StringDeserializer(), new JsonDeserializer<>(User.class, false));
        consumerServiceTest = cf.createConsumer();
        embeddedKafkaBroker.consumeFromAnEmbeddedTopic(consumerServiceTest, topic);
    }

    @Then("^I expect a new message Kafka topic (.*) Phone = (.*) Name = (.*) Status = (.*)$")
    public void testPublishSigupUserMesssage(String topicName, String phone, String name, String userStatus) {
        ConsumerRecord<String, User> consumerRecordOfExampleDTO = KafkaTestUtils.getSingleRecord(consumerServiceTest, topicName);
        User valueReceived = consumerRecordOfExampleDTO.value();

        assertThat(userStatus.replace(" ","")).isEqualTo(valueReceived.getStatus());
        assertThat(name).isEqualTo(valueReceived.getName());
        assertThat(phone).isEqualTo(valueReceived.getPhone());

        consumerServiceTest.close();
    }

    @Then("^I expect User Service consume update user message Id = (.*) Phone = (.*) Name = (.*) Status = (.*)$")
    public void testConsumerUpdateUserMesssage(int id, String phone, String name, String userStatus) {
        await().atMost(Durations.TEN_SECONDS).untilAsserted(() -> {
            User updatedUser = userRepository.findByPhone(phone);
            assertEquals(name, updatedUser.getName());
            assertEquals(phone, updatedUser.getPhone());
            assertEquals(userStatus, updatedUser.getStatus());
    }

    @Given("^User signup with Name = (.*) Phone = (.*)$")
    public void userSignUp(String name, String phone) throws Exception {
        UserSignUpForm buildUserSignUpRequest = new UserSignUpForm(name, phone);
        mvcResult = mockMvc.perform(MockMvcRequestBuilders.post("/user/sign-up")
                        .contentType(MediaType.APPLICATION_JSON)
                        .content(objectMapper.writeValueAsString(buildUserSignUpRequest)))
                .andDo(print())
                .andExpect(status().is2xxSuccessful())
                .andReturn();
    }

    private Producer<String, User> producerTest;

    @Given("^Prepare producer message Topic = (.*)$")
    public void prepareProducer(String topic){
        Map<String, Object> producerProps = KafkaTestUtils.producerProps(embeddedKafkaBroker.getBrokersAsString());
        logger.info("props {}", producerProps);
        producerTest = new KafkaProducer(producerProps, new StringSerializer(), new JsonSerializer<User>());
    }

    @Given("^There is a new Update User Status message to Topic (.*) Id = (.*) Phone = (.*) Name = (.*) Status = (.*) from Fraud Service$")
    public void newUpdateUserStatusMessage(String topic, int id, String phone, String name, String status){
        User userMessage = new User(id, name, phone, status);
        producerTest.send(new ProducerRecord(topic, "", userMessage));
        producerTest.close();
    }
}
```