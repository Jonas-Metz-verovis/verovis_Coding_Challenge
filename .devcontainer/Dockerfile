# Customized Dockerfile for a Visual Studio Code DevContainer, based on
#   https://github.com/microsoft/vscode-dev-containers/blob/v0.128.0/containers/python-3/.devcontainer/base.Dockerfile

ARG VARIANT=3.7
FROM python:${VARIANT}

# INFO: https://aka.ms/vscode-remote/containers/non-root-user
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

ARG DEFAULT_UTILS="\
    pylint \
    flake8 \
    autopep8 \
    black \
    yapf \
    mypy \
    pydocstyle \
    pycodestyle \
    bandit \
    virtualenv"
ENV PIPX_HOME=/usr/local/py-utils
ENV PIPX_BIN_DIR=${PIPX_HOME}/bin
ENV PATH=${PATH}:${PIPX_BIN_DIR}

ARG INSTALL_ZSH="true"
ARG UPGRADE_PACKAGES="true"
ARG COMMON_SCRIPT_SOURCE="https://raw.githubusercontent.com/microsoft/vscode-dev-containers/v0.128.0/script-library/common-debian.sh"
ARG COMMON_SCRIPT_SHA="a6bfacc5c9c6c3706adc8788bf70182729767955b7a5509598ac205ce6847e1e"

RUN apt-get update \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends curl ca-certificates 2>&1 \
    && curl -sSL  ${COMMON_SCRIPT_SOURCE} -o /tmp/common-setup.sh \
    && ([ "${COMMON_SCRIPT_SHA}" = "dev-mode" ] || (echo "${COMMON_SCRIPT_SHA} */tmp/common-setup.sh" | sha256sum -c -)) \
    && /bin/bash /tmp/common-setup.sh "${INSTALL_ZSH}" "${USERNAME}" "${USER_UID}" "${USER_GID}" "${UPGRADE_PACKAGES}" \
    && rm /tmp/common-setup.sh \
    && mkdir -p ${PIPX_BIN_DIR} \
    && export PYTHONUSERBASE=/tmp/pip-tmp \
    && pip3 install --disable-pip-version-check --no-warn-script-location --no-cache-dir --user pipx \
    && /tmp/pip-tmp/bin/pipx install --pip-args=--no-cache-dir pipx \
    && echo "${DEFAULT_UTILS}" | xargs -n 1 /tmp/pip-tmp/bin/pipx install --system-site-packages --pip-args=--no-cache-dir --pip-args=--force-reinstall \
    && chown -R ${USER_UID}:${USER_GID} ${PIPX_HOME} \
    && rm -rf /tmp/pip-tmp \
    && apt-get purge -y imagemagick imagemagick-6-common \
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

# Microsoft SQL Server ODBC Driver for Linux
# IMPORTANT: This RUN Command assumes that the provided Python Docker Image, see
#               https://hub.docker.com/_/python
#            is based on Debian 10 ('Buster'), change the Version in '...config/debian/10/prod...', if this isn't the Case anymore!
# INFO: For further Information, see
#   https://docs.microsoft.com/de-de/sql/connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server?view=sql-server-ver15#debian
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
#       to set up the Connection to your Databricks Development Cluster (test should return 'All tests passed.')
RUN apt-get update && \
    apt-get -y install openjdk-11-jre-headless