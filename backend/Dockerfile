# Stage 1: Build the application with Maven
FROM maven:3.8.4-openjdk-17-slim AS builder

WORKDIR /app

COPY pom.xml .
COPY src ./src

RUN mvn clean install -DskipTests

# Stage 2: Create the final image with the JAR file
FROM openjdk:17-jdk-slim

# Install PostgreSQL client
RUN apt-get update && apt-get install -y postgresql-client

WORKDIR /app

# Copy the JAR file from the builder stage
COPY --from=builder /app/target/dreamdrop-0.0.1-SNAPSHOT.jar /app.jar

EXPOSE 2424

CMD ["java", "-jar", "/app.jar"]
