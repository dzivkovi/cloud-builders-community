# Use Ubuntu 20.04 LTS as the base image
FROM ubuntu:20.04

# Avoid prompts from apt.
ENV DEBIAN_FRONTEND=noninteractive

# Install necessary packages
RUN apt-get update && \
    apt-get install -y \
    curl \
    unzip \
    bash \
    ca-certificates \
    openjdk-17-jdk-headless \
    tzdata \
    nodejs \
    npm \
    && apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install Node.js and npm
RUN curl -sL https://deb.nodesource.com/setup_18.x | bash - && \
    apt-get install -y nodejs

# Install TypeScript
RUN npm install -g typescript

# Set SonarQube Scanner environment variables
ARG SONAR_SCANNER_VERSION=5.0.1.3006
ARG SONAR_SCANNER_HOME=/opt/sonar-scanner

# Install SonarQube Scanner
RUN curl -o /tmp/sonar-scanner.zip -L https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-${SONAR_SCANNER_VERSION}-linux.zip && \
    unzip /tmp/sonar-scanner.zip -d /opt && \
    mv /opt/sonar-scanner-${SONAR_SCANNER_VERSION}-linux ${SONAR_SCANNER_HOME} && \
    rm /tmp/sonar-scanner.zip

# Update PATH environment variable
ENV PATH="${SONAR_SCANNER_HOME}/bin:${PATH}"

# Set the default working directory as /workspace
WORKDIR /workspace

# Default command on container start
CMD ["bash"]

# Build and push the image using:
# docker build -t gcr.io/$PROJECT_ID/sonar-scanner:latest .
# docker push gcr.io/$PROJECT_ID/sonar-scanner:latest

# Validate the image using:
# docker run -it -v "/$(pwd):/workspace" -e "SONAR_TOKEN=$SONAR_TOKEN" gcr.io/$PROJECT_ID/sonar-scanner:latest
