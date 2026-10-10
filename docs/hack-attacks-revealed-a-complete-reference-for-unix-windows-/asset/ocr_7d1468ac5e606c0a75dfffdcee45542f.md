**Service: Hack '99 KeyLogger**

**Hacker's Strategy:** This daemon acts as a standard key logger with one exception; it has the ability to send the attacker the target system keystrokes in real-time (see Figure 4.39).

**Port: 12345-12346**

**Service: NetBus/2/Pro**

**Hacker's Strategy:** The infamous remote administration and monitoring tool, *NetBus*, now owned by UltraAccess.net currently includes telnet, http, and real-time chat with the server. For more details, visit www.UltraAccess.net.

**Port: 17300**

**Service: Kuang**

**Hacker's Strategy:** This is a Trojan/virus mutation of a simple password retriever via SMTP.

**Port: 20000-20001**

**Service: Millenium**

**Hacker's Strategy:** Millenium is another very simple Visual Basic Trojan with remote control features that have been recently updated to include:

+   - CD-ROM control
+   - Audio control
+   - File explorer
+   - Taskbar control
+   - Desktop control
+   - Key logger
+   - Password retrieval
+   - File management
+   - Application control
+   - Browser control
+   - System shutdown/restart
+   - Audio control
+   - Port scanning

During configuration, the following registry entry is utilized:

```
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion
\RunServices - millenium
```

**Port: 21544**

**Service: GirlFriend**

**Hacker's Strategy:** This is another very common remote password retrieval Trojan. Recent compilations include messaging and FTP file access. During configuration, the following registry entry is utilized: