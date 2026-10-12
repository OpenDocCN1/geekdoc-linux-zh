![](bbox=[0.04, 0.06, 0.3, 0.37])

Figure 9-9: Access your AOL Instant Messaging using Gaim.

From the main Gaim window, you have the following options:

+   - **Accounts** — Add screen names, passwords, and options associated with your AOL Instant Messaging accounts.
+   - **Signon** — Sign on to AOL Instant Messaging by using your selected screen name.
+   - **Preferences** — Set preferences associated with AOL Instant Messaging and Chat windows. You can also load plug-ins that can perform special functions, such as spell checking and auto-reconnection.

Besides AOL IM protocols, Gaim supports other messaging protocols, including instant messaging protocols from Yahoo!, the Microsoft Network, ICQ, and IRC.

# ## Using Remote Login, Copy, and Execution

This section describes some features for allowing users to use resources across a network. They are the telnet, ssh, ftp, wget, rsync, rlogin, rcp, and rsh commands.

> **CROSS-REFERENCE:** Only the ssh service is turned on by default in Red Hat Linux. That is because the other remote login, execution, and copy commands described here do not provide encrypted communications by default, and so they can represent significant security risks. For information on how to turn on the services described in this chapter on a Red Hat Linux server, refer to Chapter 14 and Appendix C.

Two of the commands described in this section that are generally available are remote login and file transfer programs: telnet and ftp, respectively. Other commands for accessing FTP servers are ncftp and gFTP.