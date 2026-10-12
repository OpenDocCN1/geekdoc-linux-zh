# 21.11 What Find Computer does

![](bbox=[0.33, 0.11, 0.7, 0.35])

The Windows Explorer menu Tools > **Find** > **Computer** (Figure 21.14) looks for a computer that is *participating in Windows Networking* and that may or may not be displayed in the browse list. How exactly it does this depends on your machine’s and your network’s configuration. The following describes **Finding** from AliceNT, who is a member of TEST-NTD and isn’t using WINS or DNS:

+   1. when you enter a name:
+      a.  AliceNT retrieves the browse list for her domain from her segMB. If the name is in the browse list, AliceNT displays it *without trying to resolve it*. That means that the machine may not currently be accessible even though it’s displayed, e.g. if it closed down in the last 15 or 30 minutes, it may not yet have been removed from the browse list. Only when you click on the found name does AliceNT try to resolve. Figure 21.15 shows the trace generated when we looked for HAL9000-NT from AliceNT.
+   
+         Because AliceNT only looks at the browse list for her own domain, if the machine belongs to another domain, AliceNT won’t be able to find it using this mechanism
+      b. if the name isn’t in the browse list, AliceNT tries to resolve the name, using whatever name resolution methods she was configured with, e.g. if NetBIOS name resolution is enabled, AliceNT tries to resolve *name<20>* and to connect to it, using the NetBIOS session service. Note the <20> suffix (the *Server* NT service); if the machine isn’t running Server, you won’t be able to **Find** it. (You won’t be able to find a Windows-9x machine unless it is sharing files or printers.) This explains how you might be unable to **Find** a machine but still *ping* it successfully using its NetBIOS name: *ping* is resolving *name<00>*, not *name<20>*. This circumstance can easily arise if the machine you’re **Finding** is a non-Server and has been disconnected from the wire for a long time, or has just booted up: