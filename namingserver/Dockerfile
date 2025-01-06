# Use a base image with Maven and Java for building the application
FROM maven:3.8-openjdk-17 as build

# Set the working directory inside the container
WORKDIR /app

# Copy the Maven project files into the container
COPY pom.xml .
COPY src ./src

# Build the application using Maven
RUN mvn clean package -DskipTests

# Use a lighter base image for running the application
FROM openjdk:17-jdk-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the built application JAR file from the build stage
COPY --from=build /app/target/namingserver-0.0.1.jar app.jar

# Expose the application port
EXPOSE 8761

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]