# Palladio Devbox

This repository provides a pre-configured **VS Code Devcontainer** for running the Eclipse-based [Palladio Bench](https://www.palladio-simulator.com/), a software architecture simulator, on any OS that supports devcontainers. It installs all required dependencies, including Java, downloads the latest version of Palladio and makes it available as `palladio` via a wrapper script in your shell.

## Prerequisites

- **VS Code** with the **Dev Containers** extension (`ms-vscode-remote.remote-containers`) or any other IDE supporting devcontainers.
- **Podman** or **Docker** installed
- Compatibility with Wayland

## How to use

1. Add the [.devcontainer](.devcontainer) folder and its contents to a project where **palladio-devbox** should be available.
2. Considering you are using VSCode, reopen the project within the devcontainer.
3. To launch Palladio, simply type `palladio` in the devcontainer's terminal.
4. The Eclipse popup prompting you to select a workspace should pop up (Hint: The `palladio` wrapper automatically populates this with you devcontainer workspace, so configuration changes are not lost when the container is rebuilt.).
5. If you did not change the directory from `/workspaces/<your-project>`, then a `.metadata` folder, which contains the settings for you Eclipse workspace, should be created after you click "Launch".
6. Start using Palladio! 😄
