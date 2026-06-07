# Configuring Environment Variables on Windows

This topic describes how to configure the required environment variables for a local development environment installation.

1. Select **Start > Control Panel > System Properties > Environment Variables.**
2. In the **System variables** text box, ensure that the following system environment variables have been configured:

    | Environment Variable | Value    |
    | --------------------- | ------- |
    | JAVA_HOME | The location where Java JRE is installed; for example: `C:\Program Files\Java\jre1.8.0_144` |
    | ORACLE_HOME | The location where the Oracle database file is located. |
    | Path | See *[Checking Your Path Environment Variable](#checking-your-path-environment-variable)* |

## Checking Your Path Environment Variable

To ensure the Path environment variable is configured correctly:

1. In the **System Variables** text box, click the **Path** variable.
2. Click the **Edit** button.
   The **Edit Environment Variable** dialog box is displayed:

    ![Edit Environment Variable - Path](images/edit_path_env_var.png){ width="400" }
    /// caption
    Edit Environment Variable - Path
    ///

3. Ensure the following paths are added to the list:

    | Value | Description |
    | ------- | ------------- |
    | `%ORACLE_HOME%\bin` | The Oracle database bin directory |
    | `c:\windows\system32\OracleClient` | The Oracle client directory |
    | `C:\Windows` | The Windows directory |
    | `C:\Windows\System32` | The Windows system directory |
    | `C:\Windows\System32\wbem` | The Windows Management Interface (WMI) directory |
    | `C:\Program Files\Microsoft MPI\bin` | The Microsoft MPI (Message Passing Interface) bin directory |
    | `%JAVA_HOME%\bin` | The Java bin directory |
