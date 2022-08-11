FROM registry.redhat.io/ubi8/openjdk-11:latest as builder
MAINTAINER Jeganathan Swaminathan <jegan@tektutor.org>

RUN mkdir -p ./hello
COPY . ./hello
WORKDIR ./hello
RUN mvn package

FROM registry.redhat.io/ubi8/openjdk-11:latest as runner

COPY --from=builder ./app.jar ./hello/target/*.jar
CMD ["java", "-jar", "./app.jar"]
