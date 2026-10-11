# # Securing Telnet

To secure your Telnet service, do the following:

+   1. Log in to the machine you want to secure as root.
+   2. Type “vi /etc/issue.net”.
+   3. Remove all information about the operating system and version from this file.
+   4. If you want to, replace the information you removed with a different welcome message.
+   5. Other than the preceding steps, little security is possible through Telnet itself. Consider using tcp_wrappers or ipchains to control Telnet access. Press the Esc key, and then type “ZZ” to save and close the file.
+   6. Type “/etc/rc.d/init.d/inet restart” to restart the superdaemon, which handles Telnet service.

> **NOTE:** *For the best Telnet security, install the secure shell (ssh) and use its* ***stelnet*** *instead.*

| Related solutions: | Found on page: |
| --- | --- |
| Obtaining And Installing ssh | 267 |
| Restricting Network Access With tcp_wrappers | 269 |
| Setting Up ssh On A Server | 270 |
| Setting Up ssh On A Client | 276 |
| Setting Up An IP Firewall | 287 |

# # Creating A shutdown Message

To configure a **shutdown** message if you have scheduled maintenance time coming up, do the following:

+   1. Log in to the FTP server machine as root.
+   2. Type “vi /etc/shutmsg” — or the appropriate name and path if you used a different one — to open the file.
+   3. This file is empty by default. Type “i” to enter Insert mode.
+   4. You will enter your **shutdown** data in this format:

```
year month day hour minute whendeny whendisconnect message
```