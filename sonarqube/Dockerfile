FROM ubuntu:20.04

# Install Node.js
RUN apt-get update && \
    apt-get install -y curl && \
    curl -sL https://deb.nodesource.com/setup_14.x | bash - && \
    apt-get install -y nodejs

# Install Java and Maven
RUN apt-get install -y openjdk-11-jdk maven

# Verify installations
RUN java -version && \
    mvn -version && \
    node -v && \
    npm -v

WORKDIR /workspace
