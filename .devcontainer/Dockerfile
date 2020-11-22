FROM debian:buster-slim

WORKDIR /tmp

# --------------------------------
# Install Dependencies
# --------------------------------

RUN apt-get update \
    && apt-get install -y \
       wget \
       python3-pip \
       apt-transport-https \
       ca-certificates \
       curl \
       gnupg-agent \
       lsb-release \
       software-properties-common \
    && rm -rf /var/lib/apt/lists/*

# --------------------------------
# Add Keys and Repos
# --------------------------------

# Docker
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"

# Microsoft
RUN curl -fsSL https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN apt-add-repository https://packages.microsoft.com/debian/10/prod
RUN add-apt-repository https://packages.microsoft.com/repos/azure-cli/

# Update package list
RUN apt-get update

# --------------------------------
# Install packages
# --------------------------------

# Install Docker
RUN apt-get install -y docker-ce docker-ce-cli containerd.io

# Install .NET Core 3.1
RUN apt-get install -y dotnet-sdk-3.1

# Install the Azure CLI
RUN apt-get install azure-cli

# Install the Azure Functions Core Tools
RUN apt-get install azure-functions-core-tools-3

# Install IoTEdgeDev
RUN pip3 install --upgrade iotedgehubdev
