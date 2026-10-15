A return code of 0 is ideal. You might receive a return code of 4 and the message:

```
VMFP2P27601 PUT2PROD process completed with warnings
```

In general on z/VM, a return code of 4 is acceptable. That means that only warnings were issued. A return code of 8 or greater generally means that errors were encountered.

+   6. Enter the following command to shutdown and IPL your system again:
+   
+   ```text
+   ==> shutdown repl
+   SYSTEM SHUTDOWN STARTED
+   ```
+   
+   Although you lose your 3270 session, the system returns in about 2-4 minutes. After it does, the last message is:
+   
+   ```text
+   Press enter or clear key to continue
+   ```

+   7. Press Enter. The z/VM logon window opens.

Congratulations! You now have a vanilla z/VM system installed.

# Configuring the PROFILE XEDIT file

When invoked, the XEDIT command looks for the file PROFILE XEDIT configuration file. Many z/VM user IDs do not have such a personal or shared system file, so all XEDIT default values are in effect. The MAINT 191 (A) disk has a PROFILE XEDIT file, so when you are editing files on MAINT, the values in this profile are usually in effect.

To have a good experience while using XEDIT, make the profile for the MAINT user be similar to the one in Example 2-25 on page 92. To do this, log on to MAINT and edit the file with XEDIT itself:

```
==> xedit profile xedit a
```

Save your changes with the XEDIT subcommand SAVE.