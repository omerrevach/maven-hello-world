FROM maven:3.8.5-openjdk-17 as builder
WORKDIR /app
COPY pom.xml .
COPY src ./src

# Build app with maven
RUN mvn clean package -DskipTests

# part 2
FROM openjdk:17-jre-slim
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
WORKDIR /app
# copy jar file from first stage to container
COPY --from=builder /app/target/myapp-*.jar app.jar
# no root
USER appuser

CMD ["java", "-jar", "my-app.jar"] 
