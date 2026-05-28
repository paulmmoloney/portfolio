# Installing and Configuring  Elasticsearch

This topic describes how to install and configure Elasticsearch, then configure it to run as a service.

## Install Elasticsearch from Script File on Windows

1. Inside your TFS branch directory, navigate to the Elasticsearch directory.
2. Open a PowerShell or a command line window with Administrator privileges.
3. Run the script *downloadAndInstall-windows.bat*.

This script will automatically perform the following actions:

1. Download the archive for Elasticsearch 7.3.1 from online.
2. Unzip the archive into the local directory *C:\elasticsearch-7.3.1*.
3. Apply the required configurations to the file *C:\elasticsearch-7.3.1\config\elasticsearch.yml*.
4. Add the required user roles.
5. Install the required SSL certificates inside the folder *C:\elasticsearch-7.3.1\config\cert*.
6. Configure the Elasticsearch Windows service to run automatically on start-up.

## Start Elasticsearch as a Service on Windows

Elasticsearch can be run on demand from the command prompt (`\bin\elasticsearch.bat`) or as a Windows service.

The execution of the script in *Install Elasticsearch from Script File on Windows* should have installed the Elasticsearch service and configured it to run automatically on start-up. To verify this:

1. From the **Start** menu, run **Services**.
2. Check that Elasticsearch exists as a service:
    <figure markdown>
      <img src="images/es_service.png" alt="Elasticsearch Service" width="800" />
      <figcaption>Elasticsearch Service</figcaption>
    </figure>
3. Right-click on the service and select **Properties**.
4. Ensure that:
    - **Startup Type** is set to **Automatic**
    - **Status** is **Running**

## Configure Elasticsearch Indices on Windows

To configure the Elasticsearch search engine indices:

1. Navigate to `{developer_home}\PSSolution\CLM\Elasticsearch`.
2. In a text editor, edit *ConfigureElasticSearchIndices.config*.
3. Specify values for the following properties:

| Property | Value |
| ---------- | ------- |
| `<JdbcDriverLibrary>` | For Microsoft SQL Server, set to `sqljdbc42.jar`<br>For Oracle, set to `ojdbc7.jar` |
| `<JdbcDriverClass>` | For Microsoft SQL Server, set to `com.microsoft.sqlserver.jdbc.SQLServerDriver`<br>For Oracle, set to `Java::oracle.jdbc.driver.OracleDriver` |
| `<JdbcConnectionString>` | **SQL Server:**<br><br>Set to:<br>`jdbc:sqlserver://{database_server_name}[\{instance_name}];databaseName={database_name};`<br><br>Where:<br>- `{database_server_name}`: The name of the database server (from `<databaseServer>` in `{developer_home}\Setup\installer.config`)<br>- `{instance_name}`: Optional. Used if a named SQL Server instance is configured<br>- `{database_name}`: The database name (from `<databaseName>` in `{developer_home}\Setup\installer.config`)<br><br>Examples:<br>`<JdbcConnectionString>jdbc:sqlserver://FEN-LAP-479\SQL2016;databaseName=PS841;</JdbcConnectionString>`<br>`<JdbcConnectionString>jdbc:sqlserver://FEN-LAP-479;databaseName=PS841;</JdbcConnectionString>`<br><br>**Oracle:**<br><br>Set to:<br>`jdbc:oracle:thin:@{database}`<br><br>Where `{database}` is either:<br>- The TNS name, or<br>- An EZconnect string: `{host}:{port}/{servicename}`<br><br>Example:<br>`192.168.31.3:1521/orcl` |
