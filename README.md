### Eureka Server / Service Registry

1. Here we created one application where we included following two dependencies to appoint this service as a eureka server.
```groovy
implementation 'org.springframework.cloud:spring-cloud-starter'
implementation 'org.springframework.cloud:spring-cloud-starter-netflix-eureka-server'  
```

2. Apart from adding above two dependencies we need to add few other configurations as well like Dependency management and spring cloud version.
3. Apply **@EnableEurekaServer** in our main class.
4. Few other properties in application.yaml file -
```yaml
eureka:
  instance:
    hostname: localhost
  client:
    register-with-eureka: false           # these two properties defined and set to false otherwise this service
    fetch-registry: false                 # itself will be registered with eureka server, but we don't want this,
                                          # we want to register other services on this server.
server:
  port: 8761
```
5. Before regitering the microservices with eureka server, if any microservice want to contact anyone then they
need to use their host and IP Address (e.g. localhost:8080/rating), but after registering our microservices with Eureka server
there is no need for them to contact with each other using above props, they can simply use their application name.
because application name is autoatically tied-up with those by eureka server (e.g. http://Config-Server) these things we
can verify in the logs of eureka server as well when we start this server.

### Flow Diagram
![Our Eureka Server Flow Diagram](src/main/resources/images/FlowDiagram.png)

1. Microservices registered to this eureka server -
    1. [Hotel microservice](https://github.com/ayushdgupta/SpringBoot3-Hotel-Microservice).
    2. [User microservice](https://github.com/ayushdgupta/SpringBoot3-User-Microservice/tree/master).
    3. [Rating microservice](https://github.com/ayushdgupta/SpringBoot3-Rating-Microservice).
    4. [API Gateway](https://github.com/ayushdgupta/SpringBoot3-APIGateway-Microservice)