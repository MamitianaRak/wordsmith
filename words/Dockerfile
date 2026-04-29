FROM maven:alpine AS builder

COPY pom.xml .
RUN mvn verify

COPY src src
RUN mvn verify

FROM amazoncorretto:8-alpine-jdk

COPY --from=builder /target /target

CMD exec java -Xmx8m -Xms8m -jar target/words.jar
