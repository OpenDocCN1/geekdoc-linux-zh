# OffSec

```
PS: C:\Users\jeff> Enter-PSSession 1
[192.168.50.73]: PS C:\Users\jen>-Users\jen\Documents> whoami
corp\jen
```

```
[192.168.50.73]: PS C:\Users\jen\Documents> hostname
FILES04
```

Listing 838 - Inspecting the PowerShell Remoting session

Once more, we've proven that the session is originating from the target host through another lateral movement technique.

# 23.1.2 PsExec

PsExec is a very versatile tool that is part of SysInternals1142 suite developed by Mark Russinovich. It's intended to replace telnet-like applications and provide remote execution of processes on other systems through an interactive console.

In order to use this for lateral movement, a few requisites must be met. To begin, the user who authenticates to the target machine needs to be part of the Administrators local group. In addition, the ADMIN share must be available and File and Printer Sharing to be turned on. Luckily for us, the last two requirements are already met as they are the default settings on modern Windows systems.

In order to execute the command remotely, PsExec performs the following tasks:

+   - Writes psexesvc.exe into C: directory
- Creates and spawns a session on the remote host
- Runs the requested program/command as a child process of psexesvc.exe

For this scenario, let's assume we have RDP access to the offsec local administrator on CLIENT74 where we already discovered its clear-text password on FILES04.

Even though PsExec is not installed by default on Windows, we can easily transfer it on our compromised machine. For the sake of usability, the SysInternals suite is available on CLIENT74. When logged in the offsec user on CLIENT74, we can run the 64-bit version of PsExec from C.

In order to start an interactive session on the remote host, we need to invoke PsExec64.exe with the -i argument, followed by the target host and username with double passwords. We'll use corpjen as username and Nexus123! as password with the -u and -p arguments respectively. Lastly, we include the process to execute, which is a command shell in this case.

```
PS C:\Tools\SysInternals\> \PsExec64.exe -i \FILES04 -u corp\jen -p Nexus123!
cmd
```

PsExec v2.4 Execute processes remotely
Copyright (C) 2001-2022 Mark Russinovich
SysInternals - www.sysinternals.com

> 1142 (Microsoft, 2022), https://docs.microsoft.com/en-us/sysinternals/

PWK - © 2023 OffSec Services Limited. All rights reserved.

784