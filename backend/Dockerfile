# Base image
FROM openjdk:21-jdk-slim AS builder

# Set the working directory
WORKDIR /app

# Copy Gradle Wrapper and necessary configuration files
COPY gradlew gradlew.bat /app/
COPY gradle /app/gradle/
COPY build.gradle.kts settings.gradle.kts /app/
COPY src /app/src/

# Grant execute permissions and build the project
RUN chmod +x gradlew && ./gradlew build -x test --no-daemon

# Use production environment image
FROM openjdk:21-jdk-slim

# Set the working directory
WORKDIR /app

# Copy the wait-for-it.sh script
COPY wait-for-it.sh /app/wait-for-it.sh
RUN chmod +x /app/wait-for-it.sh

# Copy the JAR file from the previous stage
COPY --from=builder /app/build/libs/*.jar app.jar

# Start the application
CMD ["sh", "-c", "./wait-for-it.sh db2instance:50000 -- java -jar app.jar"]
