# Configure PowerShell

PowerShell is installed by default. Ensure that the full path to PowerShell (by default `%SYSTEMROOT%\System32\WindowsPowerShell\v1.0\`) is added to the system variable `Path`.

![PowerShell Path in Path Environment Variable](images/powershell_env_var.png){ width="400" }
/// caption
PowerShell Path in Path Environment Variable
///

## Configure PowerShell Execution Policy

1. From the **Start** menu, search for `cmd`, right-click **Command Prompt**, and select **Run as Administrator**.

2. Run the following command:

    ```bash
    c:\windows\syswow64\WindowsPowerShell\v1.0\powershell.exe -command set-executionpolicy unrestricted
    ```
