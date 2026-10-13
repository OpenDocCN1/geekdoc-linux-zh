You should be able to search through the file with vi-style commands. For example, to search for the hosts allow directive, going forward in the file, type in

```
/hosts allow
```

and press n to see the next instance of that directive. Alternatively, to search backward, type in the following:

```
?hosts allow
```

and press n to see the previous instance of that directive in the man page.

From the browser, you should be able to review Samba documentation. This lab directs you to sample stanzas for shared directories. Of course, you can browse around other Samba documentation. Learn what you need as a reference for the job, or for an exam.

# Lab 3: Configure Samba Global Settings

This lab assumes that you've backed up the smb.conf file from the /etc/samba directory.

+   1. To use SWAT, you'll first need to enable it with the associated Extended Internet Super Server. One way to do so is with the following commands:
+      # /etc/init.d/xinetd.d restart
+      # chkconfig swat on
+   2. Next, direct a browser to http://localhost:901. SWAT should prompt you for a username and password. By default, the root username and associated password will support access to SWAT.
+   3. Many administrators stick with the standard Microsoft Windows workgroup name of WORKGROUP. You can find it in the output from the smbclient -L //clientname command.
+   4. To limit access to a Samba server, you can do so in the Globals section, with the hosts allow directive. Of course, you can also do so by directly editing the smb.conf file in the /etc/samba directory.
+   5. To limit access from a specific computer, you can do so in the Globals section, with the hosts deny directive. Of course, you can also do so by directly editing the smb.conf file in the /etc/samba directory.
+   6. Make sure to click the Commit Changes button in SWAT. Then open a command line, and make Samba read the changes with the service smb reload command.
+   7. Before committing the changes, you can test them with the testparm command.

```
# /etc/init.d/xinetd.d restart
```

```
# chkconfig swat on
```