# Use Maven to build the project
FROM maven:3.9.6-amazoncorretto-21 AS build
WORKDIR /app

# Copy only the Eureka service, not the whole project
COPY eureka/pom.xml .
RUN mvn dependency:go-offline

COPY eureka/src ./src
RUN mvn package -DskipTests

# Use JDK to run the application
FROM amazoncorretto:21-alpine-jdk
WORKDIR /app

COPY --from=build /app/target/*.jar ./eureka-server.jar
EXPOSE 8761

CMD ["java", "-jar", "eureka-server.jar"]
