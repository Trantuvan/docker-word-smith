# syntax=docker/dockerfile:1

FROM maven:3.9.16-eclipse-temurin-11-alpine AS build

WORKDIR /app

# optimiza build deps out of source code
RUN --mount=type=bind,source=./pom.xml,target=./pom.xml \
    mvn verify

COPY . .
RUN mvn verify

FROM eclipse-temurin:11-jre-alpine-3.24

WORKDIR /app
EXPOSE 8080
COPY --from=build /app/target/*.jar words.jar
COPY --from=build /app/target/dependency ./dependency
CMD ["java", "-Xmx8m", "-Xms8m", "-jar", "words.jar"]