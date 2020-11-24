# verovis Visual Studio Code DevContainer
This Dockerfile can be used to create a containerized Development Environment

Last Update: 12.11.2020, Jonas Metz
Source: https://github.com/microsoft/vscode-dev-containers/tree/master/containers/python-3/.devcontainer

# Getting Started
To use this DevContainer, please
1.  Install [Docker Desktop](https://www.docker.com/products/docker-desktop) (requires Administrator Privileges)
1.  Install [Visual Studio Code](https://code.visualstudio.com/) as well as the [Remote: Containers Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
1.  Further Information about Container-based Development can be found [here](https://code.visualstudio.com/docs/remote/containers), [here](https://code.visualstudio.com/docs/remote/containers-tutorial) and [here](https://code.visualstudio.com/docs/remote/containers-advanced)
1.  Further Information about the Syntax of the [devcontainer.json](https://code.visualstudio.com/docs/remote/devcontainerjson-reference) and [Dockerfile](https://docs.docker.com/engine/reference/builder/) can be found in their respective Reference Documents
1.  Dockerfiles for other DevContainers (or Use Cases/Programming Languages) can be found in the [Visual Studio Code DevContainers GitHub Repository](https://github.com/microsoft/vscode-dev-containers/tree/master/containers)
1.  Keep in mind that the DevContainer installs all Python Packages which are listed in the Project's 'requirements.txt' File!
1.  If you plan on using Spark in the DevContainer (Databricks-Connect) you can use JDBC to connect to a Microsoft SQL Server (e.g. koalas.read_sql). The necessary Database Driver is already installed in the PySpark Environment. However (20.11.2020), for some Reason, the Spark Environment does not load other Drivers (e.g. SAP HANA) even if the .jar Files have been added to the CLASSPATH/SPARK_CLASSPATH Environment Variables or copied to the /jars Subdirectory of the PySpark Package. This also seems to be the Case if the Driver is installed via Maven on the Databricks Cluster. TODO: Check again and find a Solution! (New MS SQL Driver: https://search.maven.org/artifact/com.microsoft.sqlserver/mssql-jdbc // SAP HANA Driver: https://search.maven.org/artifact/com.sap.cloud.db.jdbc/ngdbc)

If you have any Questions, feel free to contact me ([Jonas Metz](mailto:jmetz@verovis.com)) anytime :-)