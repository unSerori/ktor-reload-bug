FROM eclipse-temurin:21-jdk-noble AS base

WORKDIR /app

COPY gradlew ./
COPY gradle/ ./gradle/
COPY build.gradle.kts ./
COPY settings.gradle.kts gradle.properties ./

# NOTE: モジュールの依存を解決する
RUN chmod +x gradlew && ./gradlew \
    dependencies \
    --no-daemon --quiet

EXPOSE 8080

CMD ["sleep", "infinity"]
