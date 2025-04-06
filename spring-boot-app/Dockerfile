<<<<<<< HEAD
=======

>>>>>>> 0b55b0d1abfdcb8bcb9fa6541bfb160763893ca0
FROM openjdk:17-alpine

# Simply the artifact path
ARG artifact=target/spring-boot-web.jar

WORKDIR /opt/app

COPY ${artifact} app.jar

# This should not be changed
ENTRYPOINT ["java","-jar","app.jar"]
