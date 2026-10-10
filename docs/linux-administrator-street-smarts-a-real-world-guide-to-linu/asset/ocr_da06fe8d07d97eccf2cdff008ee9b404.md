As with inetd, after you make changes to *xinetd*'s configuration, you must restart the super server. You do this by typing a command similar to the one used to restart *inetd*. As with that command, you can use either *reload* or *restart*, with similar effects:

```
# /etc/rc.d/init.d/xinetd restart
```

Also as with *inetd*, you may pass the *SIGHUP* signal to *xinetd* via the *kill* or *killall* command to have it reload its configuration file. This approach may be preferable if you’re using a distribution, such as Slackware, that doesn’t use a conventional *SysV* startup script to launch *xinetd*.

# ## Testing Your Configuration

After making the changes described in the last two sections, your FTP server should now be accessible. You can test it by using the text-mode *ftp* program or a GUI FTP program such as *gftp*:

```
```
$ ftp localhost
Connected to localhost (127.0.0.1),
220 www.example.com FTP server (Version 6.4/OpenBSD/Linux-ftpd-0.17) ready.
Name (localhost:rodsmith): rodsmith
334 AUTH SSL OK.
[S5L Cipher AES256-SHA]
331 Password required for rodsmith.
Password:
230-
230 User rodsmith logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```
```

You can then type FTP commands, such as *ls*, *cd*, *get*, *put*, and *exit*. (If you test using a GUI client, you’d use appropriate point-and-click operations instead.) This example shows connecting to the computer using the *localhost* interface. If successful, it proves that the server is running and accessible to the local computer; however, super server, TCP Wrappers, or FTP server configuration options could limit accesses from other computers. Thus, you should test in the same way using a remote computer as well. If you have problems with remote access, examine your configuration files for options that restrict access, such as the *only_from* option in *xinetd* or any FTP options in */etc/hosts.allow* or */etc/hosts.deny* if you use TCP Wrappers.

![](bbox=[0.14, 0.81, 0.22, 0.88])

Unless you really want to run an FTP server, remember to disable it by removing its super server configuration and reloading or restarting your super server when you’re done. Better yet, remove the FTP server package from your computer; a server that’s not installed can’t be run!