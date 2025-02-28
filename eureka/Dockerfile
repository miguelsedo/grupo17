# Build phase
FROM maven:3.9.6-amazoncorretto-21 AS build
WORKDIR /app

# Copy the POM file first (without "eureka/" in the path)
COPY pom.xml .

# Download dependencies
RUN mvn dependency:go-offline

# Copy the source code (without "eureka/")
COPY src ./src

# Build the project
RUN mvn package -DskipTests

# Run phase
FROM amazoncorretto:21-alpine-jdk
WORKDIR /app

# Copy the JAR file from the build phase
COPY --from=build /app/target/*.jar ./eureka-server.jar

# Expose the port
EXPOSE 8761

# Run the application
CMD ["java", "-jar", "eureka-server.jar"]
