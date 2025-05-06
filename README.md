# AI powered expert system demo - With Cassandra Vector DB 

Spring AI re-implementation of https://github.com/marcushellberg/java-ai-playground

This app shows how you can use [Spring AI](https://github.com/spring-projects/spring-ai) to build an AI-powered system that:

- Has access to terms and conditions (retrieval augmented generation, RAG)
- Can access tools (Java methods) to perform actions (Function Calling)
- Uses an LLM to interact with the user

![alt text](diagram.jpg)

## Requirements

- Java 17+
- OpenAI API key in `OPENAI_API_KEY` environment variable

## Running

Run the app by running `Application.java` in your IDE or `mvn` in the command line.

### Cassandra Vector Store parameters with HCD (Datastax's latest enterprise release of Cassandra)

```
spring.threads.virtual.enabled=true
spring.cassandra.contact-points=<your-contact-point>
# Port 9042 by default
spring.cassandra.port=<cassandra_port> 
spring.cassandra.local-datacenter=<dc_name>
spring.cassandra.username=hcd-superuser
spring.cassandra.password=<yourPassword>
spring.ai.vectorstore.cassandra.initialize-schema=true
```

### With OpenAI Chat

Add to the POM the Spring AI Open AI boot starter:

```xml
<dependency>
    <groupId>org.springframework.ai</groupId>
    <artifactId>spring-ai-openai-spring-boot-starter</artifactId>
</dependency>
```

Add the OpenAI configuration to the `application.properties`:

```
spring.ai.openai.api-key=${OPENAI_API_KEY}
spring.ai.openai.chat.options.model=gpt-4o
```


### With Azure OpenAI Chat

Add to the POM the Spring AI Azure OpenAI boot starter:

```xml
<dependency>
    <groupId>org.springframework.ai</groupId>
    <artifactId>spring-ai-azure-openai-spring-boot-starter</artifactId>
</dependency>
```

Add the Azure OpenAI configuration to the `application.properties`:

```
spring.ai.azure.openai.api-key=${AZURE_OPENAI_API_KEY}
spring.ai.azure.openai.endpoint=${AZURE_OPENAI_ENDPOINT}
spring.ai.azure.openai.chat.options.deployment-name=gpt-4o
```



## Build Jar

```shell
./mvnw clean install -Pproduction
```

```shell
java -jar ./target/playground-flight-booking-0.0.1-SNAPSHOT.jar
```


