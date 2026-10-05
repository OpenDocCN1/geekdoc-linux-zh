# OffSec

Before we check if Script Block Logging in PowerShell is enabled, we should always check the PowerShell history of a user. We use the Get-History cmdlet to obtain a list of commands executed in the past.

```
PS C:\Users\dave> Get-History
Get-History
```

Listing 397 - Empty result from commands were issued so far.

The output indicates that no PowerShell history was issued. At this point, we can explore how PowerShell's history works. Most Administrators use the Clear-History cmdlet to clear the PowerShell history. But this cmdlet is only clearing PowerShell's own history, which can be retrieved with Get-History. Starting with PowerShell v5, v5.1, and v7, a module named PSReadline is included, which is used for line-editing and command functionality.

Interestingly, Clear-History does not clear the command history recorded by PSReadline. Therefore, we can check if the user is in our misunderstanding the Clear-History cmdlet clears all traces of commands.

To retrieve history from PSReadline, we can use Get-PSReadlineOption to obtain information from the PSReadline module. We put it in parentheses and use HistorySavePath prepended with a syntax that allows us to check one option from all options of the module.

```
PS C:\Users\dave> Get-PSReadlineOption.HistorySavePath
(Get-PSReadlineOption).HistorySavePath
:\Users\AppData\Roaming\Microsoft\PowerShell\PSReadline\ConsoleHost_txt
```

Listing 398 - Display path of the history file from PSReadline. Let's display the contents of the file.

```
PS C:\Users\dave> type
C:\Users\AppData\Roaming\Microsoft\PowerShell\PSReadline\ConsoleHost_txt
$VersionTable
Register-SecretVault -Name pwmanager -ModuleName SecretManagement.keeppass
VaultParameters $VaultParams
Set-Secret -Name "Server02 Admin PW" -Secret "paperEarMonitor33@" -Vault pwmanager
cd C:
ls
cd C:\xampp
t passwords.txt
Clear-History
Start-Transcript -Path "C:\Users\Public\Transcripts\transcript01.txt"
```

> 769 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/powershell/module/powershell/get-history?view=powershell-7.2
775 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/powershell/module/powershell/clear-history?view=powershell-7.2
777 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/powershell/module/psreadline/view=powershell-7.2

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.