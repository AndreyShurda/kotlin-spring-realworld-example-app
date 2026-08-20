# Base image for the Kotlin + Spring Boot RealWorld API.
# Pins Maven and Temurin JDK 17 to match the project's target Java version (pom.xml java.version=17).
FROM maven:3.9-eclipse-temurin-17

# System tools required for repository checkout and general Cloud Agent use.
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        git \
        curl \
        ca-certificates \
        sudo \
    && rm -rf /var/lib/apt/lists/*

# Cloud Agents run as a non-root user; create it if the base image lacks it.
ARG USERNAME=ubuntu
RUN if ! id -u "$USERNAME" >/dev/null 2>&1; then \
        useradd --create-home --shell /bin/bash "$USERNAME"; \
    fi \
    && echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/90-$USERNAME \
    && chmod 0440 /etc/sudoers.d/90-$USERNAME

USER ubuntu
