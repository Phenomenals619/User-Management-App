# Start with a Maven build image
FROM maven:3.9.6-eclipse-temurin-17 AS build

# Set working directory inside the container
WORKDIR /app

# Copy the entire Backend project into the container
COPY . .

# Package the application (skip tests to speed up build)
RUN mvn clean package -DskipTests

# Use a lightweight Java image to run the app
FROM eclipse-temurin:17-jdk-alpine

# Set working directory
WORKDIR /app

# Copy the packaged JAR file from the previous stage
COPY --from=build /app/target/*.jar app.jar

# Expose port (must match your `application.properties` or `.yml`)
EXPOSE 8089

# Run the Spring Boot app
ENTRYPOINT ["java", "-jar", "app.jar"]
