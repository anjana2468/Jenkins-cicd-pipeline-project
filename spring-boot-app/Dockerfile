<<<<<<< HEAD
=======
# You can change this base image to anything else
# But make sure to use the correct version of Java
>>>>>>> e9c5c4c9e40e3550dabfc16461bf0ac60354ee09
FROM openjdk:17-alpine

# Simply the artifact path
ARG artifact=target/spring-boot-web.jar

WORKDIR /opt/app

COPY ${artifact} app.jar

# This should not be changed
ENTRYPOINT ["java","-jar","app.jar"]
