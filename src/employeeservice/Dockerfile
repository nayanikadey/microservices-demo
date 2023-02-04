FROM eclipse-temurin:18 as builder

WORKDIR /app

COPY ["build.gradle", "gradlew", "./"]
COPY gradle gradle
RUN chmod +x gradlew
RUN ./gradlew downloadRepos

COPY . .
RUN chmod +x gradlew
RUN ./gradlew build

FROM eclipse-temurin:18-jre-alpine

WORKDIR /app
COPY --from=builder /app .

EXPOSE 9555
# ENTRYPOINT ["java", "-jar", "./build/libs/employeeservice-1.0.jar"]
ENTRYPOINT ["java", "-javaagent:./agent/opentelemetry-javaagent.jar", "-jar", "./build/libs/employeeservice-1.0.jar"]