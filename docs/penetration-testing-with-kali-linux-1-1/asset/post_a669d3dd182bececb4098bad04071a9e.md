
## 18.2.3 User Account Control (UAC) Bypass: fodhelper.exe Case Study

UAC can be bypassed in various ways. In this first example, we will demonstrate a technique that allows an administrator user to bypass UAC by silently elevating our integrity level from medium to high.

Most of the publicly known UAC bypass techniques target a specific operating system version. In this case, the target is our lab client running Windows 10 build 1709. We will leverage an interesting UAC bypass based on **fodhelper.exe**, [507, 508] a Microsoft support application responsible for managing language changes in the operating system. Specifically, this application is launched whenever a local user selects the “Manage optional features” option in the “Apps & features” Windows Settings screen.

![](img/ec25e59d75726b7041242a56d3376832_536_0.png)

As we will soon demonstrate, the fodhelper.exe binary runs as high integrity on Windows 10 1709. We can leverage this to bypass UAC because of the way fodhelper interacts with the Windows Registry. More specifically, it interacts with registry keys that can be modified without administrative privileges. We will attempt to find and modify these registry keys in order to run a command of our choosing with high integrity.

> The Windows Registry is a hierarchical database that stores *critical information* for the operating system and for applications that choose to use it. The registry stores settings, options, and other miscellaneous information in a hierarchical tree structure of hives, keys, sub-keys, and values.

We’ll begin our analysis by running the `C:\Windows\System32\fodhelper.exe` binary, which presents the *Manage Optional Features* settings pane:

![](img/ec25e59d75726b7041242a56d3376832_537_0.png)

In order to gather detailed information regarding the fodhelper integrity level and the permissions required to run this process, we will inspect its *application manifest*. The application manifest is an XML file containing information that lets the operating system know how to handle the program when it is started. We’ll inspect the manifest with the **sigcheck** utility from Sysinternals, passing the `–a` argument to obtain extended information and `–m` to dump the manifest.

```text
C:\> cd C:\Tools\privilege_escalation\SysinternalsSuite
C:\Tools\privilege_escalation\SysinternalsSuite> sigcheck.exe –a –m C:\Windows\System32\fodhelper.exe
c:\windows\system32\fodhelper.exe:
    Verified:      Signed
    Signing date:  4:40 AM 9/29/2017
    Publisher:     Microsoft Windows
    Company:       Microsoft Corporation
    Description:   Features On Demand Helper
    Product:       Microsoft® Windows® Operating System
    Prod version:  10.0.16299.15
```

![](img/ec25e59d75726b7041242a56d3376832_538_0.png)

File version: 10.0.16299.15 (WinBuild.160101.0800)

MachineType: 32-bit

Binary Version: 10.0.16299.15

Original Name: FodHelper.EXE

Internal Name: FodHelper

Copyright: © Microsoft Corporation. All rights reserved.

Comments: n/a

Entropy: 6.306

Manifest:

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<!-- Copyright (c) Microsoft Corporation -->
<assembly
    xmlns="urn:schemas-microsoft-com:asm.v1"
    xmlns:asmv3="urn:schemas-microsoft-com:asm.v3"
    manifestVersion="1.0">
    <assemblyIdentity type="win32" publicKeyToken="6595b64144ccf1df"
        name="Microsoft.Windows.FodHelper" version="5.1.0.0"
        processorArchitecture="x86"/>
    <description>Features On Demand Helper UI</description>
    <trustInfo xmlns="urn:schemas-microsoft-com:asm.v3">
        <security>
            <requestedPrivileges>
                <requestedExecutionLevel
                    level="requireAdministrator"
                />
            </requestedPrivileges>
        </security>
    </trustInfo>
    <asmv3:application>
        <asmv3:windowsSettings
            xmlns="http://schemas.microsoft.com/SMI/2005/WindowsSettings">
            <dpiAware>true</dpiAware>
            <autoElevate>true</autoElevate>
        </asmv3:windowsSettings>
    </asmv3:application>
</assembly>
```

A quick look at the results shows that the application is meant to be run by administrative users and as such, requires the full administrator access token. Additionally, the autoelevation flag is set to true, which allows the executable to auto-elevate to high integrity without prompting the administrator user for consent.

We can use Process Monitor from the Sysinternals suite to gather more information about this tool as it executes.

> **Note:** The following content from pages 534-535 appears to be preceding text regarding integrity levels which leads into the UAC bypass section. To maintain logical flow as requested ("merge continuous paragraphs"), here is the cleaned-up preceding section:

As reported on the last line of output, this command prompt is currently operating at a Medium integrity level.

Let’s attempt to change the password for the admin user from this command prompt:

```text
C:\Users\admin> net user admin Evi@pass
System error 5 has occurred.

Access is denied.
```

The request is denied, even though we are logged in as an administrative user.

In order to change the admin user’s password, we must switch to a high integrity level even if we are logged in with an administrative user. In our example, one way to do this is through **powershell.exe** with the *Start-Process* cmdlet specifying the “Run as administrator” option:

```text
C:\Users\admin> powershell -Use Start-Process cmd.exe -Verb runAs
```

After submitting this command and accepting the UAC prompt, we are presented with a new high integrity **cmd.exe** process.

Let’s check our integrity level using the **whoami** utility using the **/groups** argument and attempt to change the password again:

```text
C:\Windows\system32> whoami /groups
GROUP INFORMATION
-------------------

Group Name                           Type            SID          Attributes
--------------------------------  --------------  ------------  -------------
Everyone                                 Well-known group S-1-1-0        Mandatory group,
NT AUTHORITY\Local account and member   Well-known group S-1-5-114     Mandatory group,
BUILTIN\Administrators                   Alias          S-1-5-32-544   Mandatory group,
BUILTIN\Users                            Alias          S-1-5-32-545   Mandatory group,
NT AUTHORITY\INTERACTIVE                 Well-known group S-1-5-4      Mandatory group,
CONSOLE LOGON                            Well-known group S-1-2-1       Mandatory group,
NT AUTHORITY\Authenticated Users            Well-known group S-1-5-11   Mandatory group,
NT AUTHORITY\This Organization              Well-known group S-1-5-15   Mandatory group,
NT AUTHORITY\Local account                    Well-known group S-1-5-113  Mandatory group,
LOCAL                                       Well-known group S-1-2-0     Mandatory group,
NT AUTHORITY\NTLM Authentication             Well-known group S-1-5-64-10 Mandatory group,
Mandatory Label\High Mandatory Level       Label                S-1-16-12288
```

```text
C:\Windows\system32> net user admin Ev!lpass
The command completed successfully.
```

This time, we are running at a high integrity level and the password change is successful.

### References

[505] (Microsoft, 2017). https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/start-process?view=powershell-6
[506] (Microsoft, 2017). https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/whoami
[509] (Winscripting blog, 2017), https://winscripting.blog/2017/05/12/first-entry-welcome-and-uac-bypass/
[510] (Microsoft, 2018), https://docs.microsoft.com/en-us/windows/win32/sysinfo/structure-of-the-registry
[511] (Microsoft, 2018), https://docs.microsoft.com/en-us/windows/win32/sysinfo/structure-of-the-registry
[512] (Microsoft, 2019), https://msdn.microsoft.com/en-us/library/windows/desktop/aa374191(v=vs.85).aspx
[513] (Microsoft, 2019), https://docs.microsoft.com/en-us/sysinternals/
[514] (Microsoft, 2010). https://msdn.microsoft.com/en-us/library/bb756929.aspx
[515] (Microsoft, 2016). https://technet.microsoft.com/en-us/library/2009.07.uac.aspx
[516] (Microsoft, 2019). https://docs.microsoft.com/en-us/sysinternals/downloads/procmon
