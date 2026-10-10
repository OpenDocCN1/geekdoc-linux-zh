![](bbox=[0.1, 0.05, 0.9, 0.45])

Figure 4.20 The NetSpy client program.

+   - Initiates messaging
+   - Hides the Start button
+   - Hides the task bar
+   - Displays an ASCII file
+   - Executes any Windows or DOS command in stealth mode

Port: 1042

Service: BLA

**Hacker's Strategy:** BLA is a remote control daemon with features that include sending ICMP echoes, target system reboot, and direct messaging (see Figure 4.21). Currently, BLA has been compiled to instantiate the following Registry keys:

```
`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run`  \n`\System = "C:\WINDOWS\System\mprdll.exe"`
```

```
`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run`  \n`\SystemDoor = "C:\WINDOWS\System\rundll argpl"`
```

95