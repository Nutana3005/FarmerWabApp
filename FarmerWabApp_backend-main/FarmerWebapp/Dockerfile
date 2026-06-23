# ---------- Build stage ----------
FROM maven:3.9.6-eclipse-temurin-21 AS build
WORKDIR /app

# Copy pom.xml and download dependencies (cache layer)
COPY pom.xml .
RUN --mount=type=cache,target=/root/.m2 mvn -B -DskipTests dependency:go-offline

# Copy source and build the JAR
COPY src ./src
RUN --mount=type=cache,target=/root/.m2 mvn -B -DskipTests clean package

# ---------- Run stage ----------
FROM eclipse-temurin:21-jre-alpine
WORKDIR /app

# Copy the fat JAR from build stage
COPY --from=build /app/target/FarmerWebapp-0.0.1-SNAPSHOT.jar app.jar

# Allow custom JVM options
ENV JAVA_OPTS=""

# Expose backend port (use 8080, since your compose maps 8084:8080)
EXPOSE 8080

# Run the Spring Boot app
ENTRYPOINT ["sh", "-c", "java $JAVA_OPTS -jar app.jar"]
