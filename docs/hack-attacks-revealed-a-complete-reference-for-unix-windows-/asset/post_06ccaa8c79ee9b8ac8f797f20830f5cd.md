
![](img/ba85bb40c695c02adae8cbd6666f2e0c_121_0.png)

**Figure 4.30** File Nail was coded to crash ICQ daemons.

- Window control
- System freeze
- Modem control
- Chat
- Audio control
- Key logging
- Printing
- Browser control

**Port:** 5001, 30303, 50505

**Service:** Sockets de Troie

**Hacker's Strategy:** The Sockets de Troie is a virus that spreads itself along with a remote administration backdoor. Once executed the virus shows a simple DLL error as it copies itself to the Windows\System\directory as MSCHV32.EXE and modifies the Windows registry. During configuration, the following registry entries are typically utilized:

```
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion
    \RunLoadMSchv32 Drv = C:\WINDOWS\SYSTEM\MSchv32.exe
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunLoad
    MgadasKdll = C:\WINDOWS\SYSTEM\MgadasKdll.exe
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunLoad
    Rsrcload = C:\WINDOWS\Rsrcload.exe
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion
    \RunServicesLoad Csctrlr132 = C:\WINDOWS\SYSTEM\Csctrlr132.exe
```

![](img/ba85bb40c695c02adae8cbd6666f2e0c_122_0.png)

**Figure 4.31** Robo-Hack limited feature base.

**Port:** 5569

**Service:** Robo-Hack

**Hacker’s Strategy:** Robo-Hack is an older remote-access backdoor written in Visual Basic. The daemon does not spread itself nor does it stay resident after system restart. The limited feature base, depicted in Figure 4.31, includes:

- System monitoring
- File editing
- System restart/shutdown
- Messaging
- Browser control
- CD-ROM control

![](img/ba85bb40c695c02adae8cbd6666f2e0c_123_0.png)

**Figure 4.32** The tHing can upload and execute programs remotely.

**Port:** 6400

**Service:** The tHing

**Hacker’s Strategy:** The tHing is a nasty little daemon designed to upload and execute programs remotely (see Figure 4.32). This daemon’s claim to fame pertains to its ability to spread viruses and other remote controllers. During configuration, the following registry entry is utilized:

```
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServices - Default
```

**Port:** 6912

**Service:** Shit Heap

**Hacker’s Strategy:** This is a fairly common Trojan that attempts to hide as your recycle bin. Upon infection, the system Recycle Bin will be updated (see Figure 4.33). The limited feature modules compiled with this Visual Basic daemon include:

![](img/ba85bb40c695c02adae8cbd6666f2e0c_123_1.png)

**Figure 4.33** System message generated after being infected by Shit Heap.

- Desktop control
- Mouse control
- Messaging
- Window killer
- CD-ROM control

**Port:** 6969, 16969

**Service:** Priority

**Hacker's Strategy:** Priority (illustrated in Figure 4.34) is a feature-rich Visual Basic remote control daemon that includes:

- CD-ROM control
- Audio control
- File explorer
- Taskbar control
- Desktop control
- Key logger
- Password retrieval
- File management
- Application control
- Browser control
- System shutdown/restart
- Audio control
- Port scanning

![](img/ba85bb40c695c02adae8cbd6666f2e0c_124_0.png)

**Figure 4.34** The feature-rich capabilities of Priority.

**Port:** 6970

**Service:** GateCrasher

**Hacker's Strategy:** GateCrasher is another dangerous remote control daemon as it masquerades as a Y2K fixer. The software contains almost every feature available in remote backdoor Trojans (see Figure 4.35). During configuration, the following registry entry is utilized:

```
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion
\RunServices - Inet
```

**Port:** 7000

**Service:** Remote Grab

**Hacker's Strategy:** This daemon acts as a screen grabber designed for remote spying. During configuration, the following file is copied:

```
\Windows\System\mprexe.exe
```

![](img/ba85bb40c695c02adae8cbd6666f2e0c_125_0.png)

**Figure 4.35** GateCrasher contains the most common backdoor features.

**Port:** 7789

**Service:** ICKiller

**Hacker's Strategy:** This daemon was designed to deliver Internet account passwords to the attacker. With a deceptive front-end, the program has swindled many novice hackers, masquerading as a simple ICQ-bomber (see Figure 4.36).

**Port:** 9400

**Service:** InCommand

**Hacker's Strategy:** This daemon was designed after the original *Sub7* series that includes a pre-configurable server module.

![](img/ba85bb40c695c02adae8cbd6666f2e0c_126_0.png)

**Figure 4.36** ICKiller is a password Stealer that masquerades as an ICQ Trojan.

**Port:** 10101

**Service:** BrainSpy

**Hacker's Strategy:** This remote control Trojan has features similar to the most typical file-control daemons; however, upon execution, the program has the ability to remove all virus scan files. During configuration, the following registry entry is utilized:

```
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServices - Dualji
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServices - Gbubuzh
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\RunServices - Fexhgcux
```

**Port:** 10520

**Service:** Acid Shivers

**Hacker's Strategy:** This remote control Trojan is based on the telnet service for command execution and has the ability to send an email alert to the attacker when the target system is active (see Figure 4.37).

![](img/ba85bb40c695c02adae8cbd6666f2e0c_126_1.png)

**Figure 4.37** Acid Shivers can send alerts to the attacker.

**Port:** 10607

**Service:** Coma

**Hacker's Strategy:** This is another remote control backdoor that was written in Visual Basic. The limited features can be deduced from the following illustration, Figure 4.38.

![](img/ba85bb40c695c02adae8cbd6666f2e0c_127_0.png)

**Figure 4.38** The limited features of Coma.

![](img/ba85bb40c695c02adae8cbd6666f2e0c_127_1.png)

**Figure 4.39** Hack '99 can send keystrokes in real-time.

**Port:** 12223

**Service:** Hack '99 KeyLogger

**Hacker's Strategy:** This daemon acts as a standard key logger with one exception; it has the ability to send the attacker the target system keystrokes in real-time (see Figure 4.39).

**Port:** 12345-12346

**Service:** NetBus/2/Pro

**Hacker's Strategy:** The infamous remote administration and monitoring tool, *NetBus*, now owned by UltraAccess.net currently includes telnet, http, and real-time chat with the server. For more details, visit www.UltraAccess.net.

**Port:** 17300

**Service:** Kuang

**Hacker's Strategy:** This is a Trojan/virus mutation of a simple password retriever via SMTP.

**Port:** 20000-20001

**Service:** Millenium

**Hacker's Strategy:** Millenium is another very simple Visual Basic Trojan with remote control features that have been recently updated to include:

- CD-ROM control
- Audio control
- File explorer
- Taskbar control
- Desktop control
- Key logger
- Password retrieval
- File management
- Application control
- Browser control
- System shutdown/restart
- Audio control
- Port scanning

During configuration, the following registry entry is utilized:

```
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion
\RunServices - millenium
```

**Port:** 21544

**Service:** GirlFriend

**Hacker's Strategy:** This is another very common remote password retrieval Trojan. Recent compilations include messaging and FTP file access. During configuration, the following registry entry is utilized:

```
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion
\RunServices − Windll.exe
```

**Port:** 22222, 33333

**Service:** Prosiak

**Hacker’s Strategy:** Again, another common remote control Trojan with standard features including:

- CD-ROM control
- Audio control
- File explorer
- Taskbar control
- Desktop control
- Key logger
- Password retrieval
- File management
- Application control
- Browser control
- System shutdown/restart
- Audio control
- Port scanning

During configuration, the following registry entry is utilized:

```
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion
\RunServices − Microsoft DLL Loader
```

**Port:** 30029

**Service:** AOL Trojan

**Hacker’s Strategy:** Basically, the AOL Trojan infects DOS .EXE files. This Trojan can spread through local LANs, WANs, the Internet, or through email. When the program is executed, it immediately infects other programs.

**Port:** 30100-30102

**Service:** NetSphere

**Hacker’s Strategy:** This is a powerful and extremely dangerous remote control Trojan with features such as:

- Screen capture
- Messaging
- File explorer
- Taskbar control
- Desktop control
- Chat
- File management
