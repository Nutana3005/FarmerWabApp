# Stage 1: Build with Maven + Java 21
FROM maven:3.9.6-eclipse-temurin-21 AS build
WORKDIR /app
COPY . .
RUN mvn clean package -DskipTests

# Stage 2: Run Spring Boot JAR with Java 21
FROM eclipse-temurin:21-jdk
WORKDIR /app
COPY --from=build /app/target/FarmerWebapp-0.0.1-SNAPSHOT.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
