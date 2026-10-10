# 8.3. PRINTER CONFIGURATION

![](bbox=[0.11, 0.13, 0.84, 0.49])

Figure 8.8: Configuring a Print Filter

+   * **Printer Name:** Name of the printer on which you want to print.
+   * **User:** Name of user you must login as to access the printer (typically guest for Windows servers, or nobody for samba servers).
+   * **Password:** Password (if required) to use the printer (typically blank). Someone should be able to tell you this if you do not already know it.

**Please Note:** If you need to use a username and password for an SMB (LAN Manager) print queue, they are stored unencrypted in a local script and must be passed on the command line to the smbclient program. Thus, it is possible for another person to learn the username and password. It is therefore recommended that the username and password for use of the printer not to be the same as that for a user account on the local Red Hat Linux system, so that the only possible security compromise would be unauthorized use of the printer. If there are file shares from the SMB server, it is recommended that they also use a different password than the one for the print queue.