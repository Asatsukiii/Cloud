# ===== BUILD STAGE =====
FROM eclipse-temurin:21-jdk-alpine AS build

WORKDIR /app
RUN apk add --no-cache maven

# Copy project files
COPY pom.xml .
COPY src ./src

# Build the JAR (skip tests)
RUN mvn clean package -DskipTests

# ===== RUNTIME STAGE =====
FROM eclipse-temurin:21-jre-alpine

WORKDIR /app

# Copy the compiled JAR from the build stage
COPY --from=build /app/target/*.jar app.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
