# Backend Dockerfile (multi-stage build)
FROM maven:3.9.4-eclipse-temurin-21 AS build
WORKDIR /workspace
COPY pom.xml ./
COPY src ./src
# package the application (skip tests to speed up)
RUN mvn -B -DskipTests package

FROM eclipse-temurin:21-jre-alpine
WORKDIR /app
# copy the built jar (assumes spring-boot-maven-plugin produces a single jar in target)
COPY --from=build /workspace/target/*.jar app.jar
EXPOSE 1430
ENTRYPOINT ["java","-jar","/app/app.jar"]
