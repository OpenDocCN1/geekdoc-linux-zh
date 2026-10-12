From the main Gaim window, you have the following options:

+   -   **Quit** — Exit from Gaim.
+   -   **Accounts** — Add screen names, passwords, and options associated with your AOL Instant Messaging accounts.
+   -   **Signon** — Sign on to AOL Instant Messaging by using your selected screen name.
+   -   **About** — Displays information about GAIM and its creators.
+   -   **Options** — Set options associated with AOL Instant Messaging and Chat windows.
+   -   **Plug-ins** — Load plug-ins that can perform special functions, such as spell checking and auto-reconnection.

Besides AOL IM protocols, Gaim supports other messaging protocols, including instant messaging protocols from Yahoo!, the Microsoft Network, ICQ, and IRC.

# ## Using Remote Login, Copy, and Execution

This section describes some features for allowing users to use resources across a network. They are the *telnet*, *ssh*, *ftp*, *wget*, *rsync*, *rlogin*, *rcp*, and *rsh* commands.

> **CROSS-REFERENCE:** Because using these commands can represent significant security risks, Red Hat Linux is not configured to allow any of these commands to connect to it by default. For information on how to turn on these services on a Red Hat Linux server, refer to Chapter 14 (Computer Security Issues) and Appendix C (Running Network Services).

There is a nice set of commands available with Red Hat Linux for moving information between computers on a network — particularly between trusted computers. Two of the commands described in this section that are generally available are remote login and file transfer programs: *telnet* and *ftp*, respectively. Other commands for accessing FTP servers are *ncftp* and *gFTP*.

Two newer commands for copying files over the network are *wget* and *rsync*. Both of these tools can be used for efficiently downloading files that you can identify on the network.

Other commands described in this section are more specific to Red Hat Linux and other UNIX systems, but provide simplified ways of copying files, logging in, and executing commands among trusted systems: *rcp*, *rlogin*, and *rsh*, respectively. Also, a more secure tool for remote login called *ssh* has recently been added to the Red Hat Linux distribution. The *ssh* command can be used for remote execution as well.

# ## Using telnet for remote login

*Telnet* is a service provided by many different types of computer systems to enable remote users to log in to their machines over TCP/IP networks. The *telnet* command is the client