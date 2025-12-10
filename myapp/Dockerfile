FROM maven:3.8.5-openjdk-17 as builder
WORKDIR /app
COPY pom.xml .
COPY src ./src

# Build app with maven
RUN mvn clean package -DskipTests

# part 2
FROM eclipse-temurin:17-jre-alpine
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
WORKDIR /app
# copy jar file from first stage to container
COPY --from=builder /app/target/myapp-*.jar app.jar
# no root
USER appuser

ENTRYPOINT ["java", "-jar", "app.jar"]
