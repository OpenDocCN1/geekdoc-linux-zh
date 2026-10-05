# # OffSec Penetration Testing with Kali Linux

| d---- | 7/20/2022 | 8:07 AM | windows |
| d---- | 6/16/2022 | 1:17 PM | xampp |

Listing 403 - Using evil-winrm to connect CLIENTWLK220 as daveadmin

As Listing 403 shows, we can enumerate commands without any issues. Great!

PowerShell artifacts such as the history file of PSRedline or transcript files are a trove of valuable information. We should never skip reviewing them, because most Administrators clear their history with Clear-History and therefore, the PSRedline history stays untouched for us to analyze.

Administrators can prevent PSRedline from recording commands by setting the HistorySaveStyle to SaveNothing with the Set-PSRedlineOption79 Cmdlet. Alternatively, they can clear the history file manually.

In this section, we explored PowerShell Transcriptions as powerful mechanisms to record commands and scripts in PowerShell. In addition, we discussed and how PowerShell saves this history. We used this knowledge in an example to obtain a password for another system as well as the password for the administrative user daveadmin.

# ## 16.5 Automated Enumeration

In the previous sessions, we manually enumerated CLIENTWLK220. We gathered information, which led us to two different ways to elevate our privileges. However, this took some time to do. In a real-life penetration test for a client, we have time constraints, limiting the time we can take to enumerate systems in a manual way.

Therefore, we used automated tools that enumerate the target machine and provide results about situational awareness as well as potential sensitive information in an easy to consume fashion. One tool is winPEAS780.

> Automated tools can be blocked by AV solutions. If this is the case, we can apply techniques learned in the Module "Antivirus Evasion", try other tools as Seatbelt781 and JAWS782, or do the enumeration manually.

As Kali already includes winPEAS, we can copy the 64-bit binary to our home directory and start a Python3 server to serve it.

```
kali@:- cp /usr/share/peas/winpeas/winPEASx64.exe
```

```
kali@:- python3 -m http.server 80
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
```

Listing 404 - Copy winPEAS to our home directory and start Python server

779 (Microsoft Documentation, 2022), https://learn.microsoft.com/en-us/powershell/module/psredline/psredlineoption-view=powershell-7-2
780 (GitHub, 2022), https://github.com/carlosopop/PEAS-ng/tree/master/winPEAS
781 (GitHub, 2022), https://github.com/GhostPack/Seatbelt
782 (GitHub, 2022), https://github.com/411hall/JAWS

PWK - Copyright ©2023 OffSec Services Limited. All rights reserved.