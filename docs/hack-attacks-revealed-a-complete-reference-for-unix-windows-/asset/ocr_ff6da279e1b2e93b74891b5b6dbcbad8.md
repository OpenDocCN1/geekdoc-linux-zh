![](bbox=[0.13, 0.05, 0.71, 0.38])

**Figure 4.32** The tHing can upload and execute programs remotely.

**Port: 6400**

**Service:** The tHing

**Hacker’s Strategy:** The tHing is a nasty little daemon designed to upload and execute programs remotely (see Figure 4.32). This daemon’s claim to fame pertains to its ability to spread viruses and other remote controllers. During configuration, the following registry entry is utilized:

```
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\RunServices - Default
```

**Port: 6912**

**Service:** Shit Heap

**Hacker’s Strategy:** This is a fairly common Trojan that attempts to hide as your recycle bin. Upon infection, the system Recycle Bin will be updated (see Figure 4.33). The limited feature modules compiled with this Visual Basic daemon include:

![](bbox=[0.13, 0.72, 0.38, 0.81])

**Figure 4.33** System message generated after being infected by Shit Heap.

+   - Desktop control
+   - Mouse control
+   - Messaging
+   - Window killer