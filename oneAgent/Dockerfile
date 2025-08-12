from ubuntu:22.04
# Install dependencies

USER root

RUN apt-get update && \
    apt-get install -y wget curl gnupg2 lsb-release && \
    rm -rf /var/lib/apt/lists/* \

# Set environment variables for Dynatrace OneAgent
ENV ONEAGENT_INSTALLER_VERSION=1.0.0 \
    ONEAGENT_INSTALLER_URL=https://your-dynatrace-installer-url.com/
# Download and install Dynatrace OneAgent
RUN wget -O Dynatrace-OneAgent.sh $ONEAGENT_INSTALLER_URL && \
    chmod +x Dynatrace-OneAgent.sh && \
    ./Dynatrace-OneAgent.sh --set-app-log-content-access=true --set-host-group=default --set-host-name=default && \
    rm Dynatrace-OneAgent.sh \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean

#setting up the entrypoint \
ENTRYPOINT ["/opt/dynatrace/oneagent/agent/bin/oneagentctl", "start"]

# Expose necessary ports
EXPOSE 443 80
# Set the working directory
WORKDIR /opt/dynatrace/oneagent
# Copy any necessary files (if needed)
