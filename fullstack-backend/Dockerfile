# AS <NAME> to name this stage as maven
FROM maven:latest AS maven
LABEL MAINTAINER="jd.ramkumar@gmail.com"

WORKDIR /usr/src/app
COPY . /usr/src/app
RUN --mount=type=cache,target=/root/.m2 mvn -f /usr/src/app/pom.xml clean package -Dmaven.test.skip=true

FROM mcr.microsoft.com/openjdk/jdk:17-ubuntu

ARG JAR_FILE=fullstack-backend-0.0.1-SNAPSHOT.jar

WORKDIR /opt/app

COPY --from=maven /usr/src/app/target/${JAR_FILE} /opt/app/

ENTRYPOINT ["java","-jar","fullstack-backend-0.0.1-SNAPSHOT.jar"]