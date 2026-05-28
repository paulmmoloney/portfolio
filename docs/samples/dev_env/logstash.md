# Installing Logstash

Logstash is a data loader which can pull data from several sources and push that data into an Elasticsearch index.

To install Logstash on Windows:

1. Define the `LS_JAVA_OPTS` environment variable required by Logstash:

    - Select **Start > Control Panel > System Properties > Environment Variables**.
    - In the **System Variables** pane, click **New** and add a new variable named `LS_JAVA_OPTS`.

2. Set `LS_JAVA_OPTS` to the following value:

    - If using Microsoft SQL Server: `-Duser.timezone=UTC`
    - If using Oracle: `-Doracle.net.tns_admin=C:\OracleService\product[Version][db_path]\NETWORK\ADMIN -Duser.timezone=UTC`

3. Download the archive `logstash-7.3.1.zip` from:
   [https://www.elastic.co/downloads/past-releases/logstash-7-3-1](https://www.elastic.co/downloads/past-releases/logstash-7-3-1)

4. Right-click `logstash-7.3.1.zip` and select **7-Zip > Extract Files…**, then extract to `C:\`.

After this, you should have a folder at `C:\logstash-7.3.1`.
