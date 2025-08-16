# Stage 1: Build with Maven
FROM maven:3.8.4-openjdk-11 AS builder

WORKDIR /app

# Copy pom.xml and download dependencies (cache layer)
COPY pom.xml .

RUN mvn dependency:go-offline

# Copy source code
COPY src ./src

# Build the project and create a jar (adjust if your packaging is different)
RUN mvn clean package -DskipTests

# Stage 2: Run the app
FROM openjdk:11-jre-slim

WORKDIR /app

# Copy the jar from the builder stage
COPY --from=builder /app/target/*.jar app.jar

# Run the jar
CMD ["java", "-jar", "app.jar"]
