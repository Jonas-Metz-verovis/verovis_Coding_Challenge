# verovis Visual Studio Code DevContainer
This Dockerfile can be used to create a containerized Development Environment

Last Update: 12.11.2020, Jonas Metz
Source: https://github.com/microsoft/vscode-dev-containers/tree/master/containers/python-3/.devcontainer

# Getting Started
To use this DevContainer, please
1.  Install [Docker Desktop](https://www.docker.com/products/docker-desktop) (requires Administrator Privileges)
2.  Install [Visual Studio Code](https://code.visualstudio.com/) as well as the [Remote: Containers Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
3.  Further Information about Container-based Development can be found [here](https://code.visualstudio.com/docs/remote/containers), [here](https://code.visualstudio.com/docs/remote/containers-tutorial) and [here](https://code.visualstudio.com/docs/remote/containers-advanced)
4.  Further Information about the Syntax of the [devcontainer.json](https://code.visualstudio.com/docs/remote/devcontainerjson-reference) and [Dockerfile](https://docs.docker.com/engine/reference/builder/) can be found in their respective Reference Documents
5.  Dockerfiles for other DevContainers (or Use Cases/Programming Languages) can be found in the [Visual Studio Code DevContainers GitHub Repository](https://github.com/microsoft/vscode-dev-containers/tree/master/containers)
6.  Keep in mind that the DevContainer installs all Python Packages which are listed in the Project's 'requirements.txt' File!
7.  Also, currently (12.11.2020) it somehow doesn't seem to be possible to use Git Version Control if the Folder is reopened in the Container (Docker with Hyper-V Backend). If you want to commit your Changes, reopen the Folder locally or use Git to clone the Repository directly inside of the Container

If you have any Questions, feel free to contact me ([Jonas Metz](mailto:jmetz@verovis.com)) anytime :-)