FROM registry.redhat.io/ubi8/openjdk-11:latest as build
MAINTAINER Jeganathan Swaminathan <jegan@tektutor.org>

COPY * /hello
WORKDIR /hello

RUN mvn package

FROM registry.redhat.io/ubi8/openjdk-11:latest as run
COPY --from=build /hello/target/*.jar ./app.jar

CMD ["java", "-jar", "./app.jar"]
