# INFO: Customized Dockerfile (12.11.2020) for a Visual Studio Code DevContainer, based on
#   https://raw.githubusercontent.com/microsoft/vscode-dev-containers/master/containers/python-3/.devcontainer/Dockerfile
# which is based on
#   https://raw.githubusercontent.com/microsoft/vscode-dev-containers/master/containers/python-3/.devcontainer/base.Dockerfile
# and is using these Scripts
#   https://github.com/microsoft/vscode-dev-containers/tree/master/containers/python-3/.devcontainer/library-scripts

ARG VARIANT=3.7
FROM mcr.microsoft.com/vscode/devcontainers/python:${VARIANT}

ARG INSTALL_NODE="true"
# ARG NODE_VERSION="lts/*"
# INFO: If you plan to use the SAP HANA SQLTools Extension, currently only Node.js 12 is supported!
ARG NODE_VERSION="12.19.0"

RUN if [ "${INSTALL_NODE}" = "true" ]; then su vscode -c "source /usr/local/share/nvm/nvm.sh && nvm install ${NODE_VERSION} 2>&1"; fi

# INFO: Uncomment this Section to install additional Debian Packages
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

# INFO: Uncomment this Section to install global Node.js Packages
# RUN su vscode -c "source /usr/local/share/nvm/nvm.sh && npm install -g <your-package-here>" 2>&1

# INFO: If you plan to use the SAP HANA SQLTools Extension, you need to install the SAP HANA Node.js Package!
#       Due to the Fact that the SAP HANA Node.js Driver Installation of SQLTools fails (for some reason), it will be copied from the global Node.js Library instead.
RUN su vscode -c "source /usr/local/share/nvm/nvm.sh && npm install -g @sap/hana-client@latest" 2>&1
RUN mkdir -p /root/.local/share/vscode-sqltools/node_modules && \
    cp -r /usr/local/share/nvm/versions/node/v${NODE_VERSION}/lib/node_modules/@sap /root/.local/share/vscode-sqltools/node_modules

# Microsoft SQL Server ODBC Driver for Linux
# IMPORTANT: This RUN Command assumes that the Python Docker Image, see
#               https://hub.docker.com/_/python
#            used by
#               https://raw.githubusercontent.com/microsoft/vscode-dev-containers/master/containers/python-3/.devcontainer/base.Dockerfile
#            is based on Debian 10 ('Buster'), change the Version in '...config/debian/10/prod...', if this isn't the Case anymore!
# INFO: For further Information, see
#       https://docs.microsoft.com/de-de/sql/connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server?view=sql-server-ver15#debian
RUN apt-get update && \
    apt-get -y install curl && \
    curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
    curl https://packages.microsoft.com/config/debian/10/prod.list > /etc/apt/sources.list.d/mssql-release.list && \
    apt-get update && \
    ACCEPT_EULA=Y apt-get -q -y install msodbcsql17 && \
    apt-get -y install unixodbc-dev

# INFO: To be able to use Databricks-Connect, the Java Runtime Environment must be installed!
#       Even though Databricks-Connect warns that 'Java versions >8 are not supported by this SDK', starting with Spark 3.0, Java 11 is supported.
#       Start a Terminal in the DevContainer and use 'databricks-connect configure' and 'databricks-connect test'
#       to set up the Connection to your Databricks Development Cluster (test should return 'All tests passed.'), see
#       https://docs.databricks.com/dev-tools/databricks-connect.html#step-2-configure-connection-properties
RUN apt-get update && \
    apt-get -y install openjdk-11-jre-headless