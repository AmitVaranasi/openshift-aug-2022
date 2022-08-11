FROM registry.redhat.io/ubi8/openjdk-11:latest as builder
MAINTAINER Jeganathan Swaminathan <jegan@tektutor.org>

RUN mkdir -p ./hello
COPY . ./hello
WORKDIR ./hello
COPY ./hello/target/spring-hello-1.0.jar /tmp/app.jar
RUN mvn package

FROM registry.redhat.io/ubi8/openjdk-11:latest as runner

COPY --from=builder /tmp/app.jar .
CMD ["java", "-jar", "./app.jar"]
