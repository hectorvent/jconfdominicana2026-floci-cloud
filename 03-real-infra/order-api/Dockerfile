# Runtime-only image. The setup script runs `mvn package` on the host first
# (you already have Java 21 + Maven, and a warm Maven cache from Modules 1-2),
# then this copies the Quarkus fast-jar layout into a slim JRE. One small layer,
# no Maven-in-Docker, no second dependency download.
FROM eclipse-temurin:21-jre-alpine
WORKDIR /app

COPY target/quarkus-app/lib/     ./lib/
COPY target/quarkus-app/*.jar    ./
COPY target/quarkus-app/app/     ./app/
COPY target/quarkus-app/quarkus/ ./quarkus/

RUN addgroup -S app && adduser -S app -G app && chown -R app:app /app
USER app

EXPOSE 8080
ENV QUARKUS_HTTP_HOST=0.0.0.0
ENTRYPOINT ["java", "-jar", "quarkus-run.jar"]
