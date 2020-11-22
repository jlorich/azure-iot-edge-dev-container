# Azure IoT Edge Dev Container

This repository contains the build and configuration files designed to be used as a [Visual Studio Code Dev Container](https://code.visualstudio.com/docs/remote/containers) for [Azure IoT Edge](https://azure.microsoft.com/en-us/services/iot-edge/) development.

## Why a dev container?

VS Code Development Containers provide a way to package up everything needed for effective development on a project into one single package.  This provides a uniform experience for *all* developers working on the project, helping avoid the dreaded "well, it works on my machine".

Development containers are absolutely the future of development environments, and even are the foundation for getting thigns to workin projects like [GitHub Codespaces](https://github.com/features/codespaces).

## Using this project

To use this dev container, simply [install Visual Studio Code](https://code.visualstudio.com/download) along with the [`remote-containers` extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) and include the `.devcontainer/devcontainer.json` file from this repo in your project. The container itself is pre-built and published to [Docker Hub](https://hub.docker.com/repository/docker/azureiotgbb/iot-edge-dev-container).

If you wish to customize the container yourself, you can choose to include the `Dockerfile` fom this repo and replace the `image` property in `devcontainer.json` with `"dockerFile": "Dockerfile"`.  Once you do this, choosing `>Remote-Containers:Rebuild Container` in the VS Code Command Pallet will build the container locally using whatever you've included in the `Dockerfile`.


## Included components

This development container includes a number of common packages useful for IoT Edge development including:

- [IoT EdgeHub Dev Tool](https://github.com/Azure/iotedgehubdev)
- [.NET 3.1 SDK](https://dotnet.microsoft.com/download/dotnet-core/3.1)
- [Azure Functions Core Tools](https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local?tabs=linux%2Ccsharp%2Cbash)
- [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
- [Docker CLI](https://docs.docker.com/engine/reference/commandline/cli/)
- [Git](https://git-scm.com/)

## Configuraiton, credentials, and more

#### Docker
`devcontainer.json` includes a mount to your hosts [Docker Daemon Socket](https://docs.docker.com/engine/reference/commandline/dockerd/#daemon-socket-option), meaning all `docker` commands (including everything managed by the IoT Edge Hub Dev Simulator) run will actually execute on the *host*.  This ensures flexibility and performance.

Because we're running all our containers against the host, it's important to note that any Volume mounts specified within IoT Edge need to be paths on the host file system.  On Linux development this is mostly irrelevant, however if you're using [Docker Desktop with the WSL2 Backend](https://docs.docker.com/docker-for-windows/wsl/) this means your volumes will exist on the Windows filesystem.

#### Azure CLI

The `devcontainer.json` file includes a mount for the `.azure` folder inside your user's home directory.  This mount will forward your local Azure CLI credentials and configuration from your host into the dev container.

#### Git

The VS Code remote-containers extension will automatically handle forwarding of credentials for https git repos from your host.  If you're using SSH auth for your git repos, see the SSH section below.

#### SSH 

SSH Keys are not shared with a simple volume mount, however the VS Code remote-containers extension will forward the contents of the `ssh-agent` running on the host.  You can configure this and add keys by following [these steps](https://code.visualstudio.com/docs/remote/containers#_sharing-git-credentials-with-your-container).

## Contributions
See something you think is missing or an update that needs to be made? Please feel free to submit a pull request!