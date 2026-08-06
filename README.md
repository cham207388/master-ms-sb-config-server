# Config Server

- resources/config/application-name.yml
- resources/config/application-name-profile.yml
- [see info](http://localhost:8071/application-name)

---

## encrypt|decrypt

add an `encrypt.key` property to your `application.properties` or `application.yml` file.

- [resource](https://docs.spring.io/spring-cloud-config/docs/current/reference/html/#_encryption_and_decryption
- [encrypt](http://localhost:8071/encrypt)
- [decrypt](http://localhost:8071/decrypt)

## refresh

**manual refresh: by every client**

- needs actuator dependency
- POST: /actuator/refresh 
  - refresh is not exposed by default, 
  - you need to add `management.endpoints.web.exposure.include=refresh` to your `application.properties` or `application.yml` file)
  - refresh endpoint to be invoked by each client

**Using Spring Cloud Bus: manual by only one client**

- requires rabbit mq or Kafka instance
- add *spring-cloud-starter-bus-amqp* dependency to your **config server** and **config client**
- refresh endpoint to be invoked by only one client

**automatic refresh**

- add *spring-cloud-starter-bus-monitor* dependency to your **config server**
- you need to add `management.endpoints.web.exposure.include=refresh`
- create web hook to your git repository, and point it to your config server refresh endpoint
- hookdeck.com (webhook testing service) can be used to test the web hook