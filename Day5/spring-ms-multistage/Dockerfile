FROM registry.redhat.io/ubi8/openjdk-11:latest as build
MAINTAINER Jeganathan Swaminathan <jegan@tektutor.org>

RUN mkdir -p ./hello

COPY * ./hello

WORKDIR ./hello

RUN mvn package

FROM registry.redhat.io/ubi8/openjdk-11:latest as run
COPY --from=build ./app.jar ./hello/target/*.jar

CMD ["java", "-jar", "./app.jar"]
