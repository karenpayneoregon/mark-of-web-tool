# Mark of the web remover

![s](assets/MarkOfTheWeb.png)

A utility to remove `mark of the web` from a folder recursively to all sub-folders.

If after downloading and un-zipping a archive file with perhaps a Visual Studio solution the files extracted may have been blocked, with this utility close Visual Studio, run this utility on the folder than re-open Visual Studio.

Current arguments (change to suite your environment)

**Base code**

```csharp
public static void UnblockFiles(string folderName)
{
    if (!Directory.Exists(folderName))
    {
        return ;
    }

    var start = new ProcessStartInfo
    {
        FileName = "powershell.exe",
        RedirectStandardOutput = true,
        Arguments = $"Get-ChildItem -Path '{folderName}' -Recurse | Unblock-File",
        CreateNoWindow = true, 
        UseShellExecute = false
    };

    using var process = Process.Start(start);
    process.WaitForExit();
}
```



##  Tool

Without this tool a developer must right click on each and every file, go to properties and un-check mark of the web and click apply or write a PowerShell script (this tool uses PowerShell).

The only drawback is perhaps forgetting the tool name which is easy here. From a command window or PowerShell window type `dotnet tool list --global` and press <kbd>enter</kbd>.

![x](assets/toolList.png)

After the tool runs all files that may had mark of the web are devoid of mark of the web including all sub-folders.

### Install/uninstall

```
dotnet tool install --global --add-source ./nupkg MarkOfTheWeb
dotnet tool uninstall -g MarkOfTheWeb
```

#### Run without arguments

![Noargs](assets/noargs.png)


#### Run with arguments

Here a .zip file was downloaded and files extracted which at that point several files had mark of the web.

![Using](assets/using.png)


# Install from Nuget

```
dotnet tool install --global MarkOfTheWeb --version 1.0.1
```