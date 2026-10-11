+   Server role: ROLE_STANDALONE
+   Press enter to see a dump of your service definitions
+   ...
+   If you misspell a keyword in smb.conf, you get an error such as the following:
+   ```
+   # testparm
+   Load smb config files from /etc/samba/smb.conf
+   Unknown parameter encountered: "workgroup"
+   Ignoring unknown parameter "workgroup"
+   ...
+   ```

ping

+   3. Use ping (page 379) from both sides of the connection to make sure the network is up.

net view

+   4. From a Windows command prompt, use net view to display a list of shares available from the server (pb in this example):
+   ```text
+   C:>net view \\pb
+   Shared resources at \\pb
+   
+     pb  Samba
+   
+    Share name    Type    Used as    Comment
+   -------------------------------------------------------------------------------
+     MainPrinter  Print   MainPrinter
+     mark         Disk    (UNC)    Home Directories
+     tmp          Disk             mys temp
+   The command completed successfully.
+   ```

net use

+   5. Try to map the drive from a Windows command prompt. The following command attempts to mount the share named tmp on pb as drive X:
+   ```text
+   C:>net use x: \\pb\tmp
+   The command completed successfully.
+   ```

nmblookup

+   6. From the server, query the nmbd server, using the special name __SAMBA__ for the server’s NetBIOS name. The -d 2 option turns the debugger on at level 2, which generates a moderate amount of output:
+   ```bash
+   $ nmblookup -d 2 -B pb __SAMBA__
+     added interface ip=192.168.0.10 bcast=192.168.0.255
+       nmask=255.255.255.0
+     querying __SAMBA__ on 192.168.0.10
+     Got a positive name query response from 192.168.0.10 ( 192.168.0.10 <0>)
+     192.168.0.10  __SAMBA__<0>
+   ```

nmblookup

+   7. From the server, query the nmbd server for the client’s NetBIOS name. (The machine named jam is the Windows client.)
+   ```bash
+   $ nmblookup -B jam \>
+     querying 0 on 192.168.0.9
+     192.168.0.9  <0>
+   ```

Omit the -B jam option to query for all NetBIOS names.