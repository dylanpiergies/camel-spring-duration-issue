# Demonstration of Duration property binding issue with camel-azure-servicebus-starter

This project provides a minimal reproduction of an issue observed where adding the dependency:

```groovy
implementation 'org.apache.camel.springboot:camel-azure-servicebus-starter:4.4.0'
```

to `build.gradle` causes Spring Boot to fail to bind application properties of type `java.time.Duration` correctly.

When running the application we see:

```
2024-03-08T10:08:21.008Z  INFO 673817 --- [           main] org.example.Application                  : Configured duration is null
2024-03-08T10:08:21.008Z  INFO 673817 --- [           main] org.example.Application                  : Configured inner duration is null
```

but if we comment out the camel-azure-servicebus dependency in `build.gradle` and rebuild we see the expected output:

```
2024-03-08T10:09:19.544Z  INFO 674032 --- [           main] org.example.Application                  : Configured duration is PT1H
2024-03-08T10:09:19.545Z  INFO 674032 --- [           main] org.example.Application                  : Configured inner duration is PT2H
```
