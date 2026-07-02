FROM eclipse-temurin:21-jdk-noble AS base

WORKDIR /app

EXPOSE 8080

CMD ["bash", "-c", "./gradlew -t build -x test -i & ./gradlew run"]
