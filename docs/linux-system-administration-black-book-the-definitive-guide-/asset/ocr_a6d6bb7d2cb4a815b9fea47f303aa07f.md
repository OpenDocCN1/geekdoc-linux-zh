+   19. Cursor down to:
+   
+       ```
+       shutdown /etc/shutmsg
+       ```

+   20. If you do not intend to use this feature, comment the line out. If you do intend to use it, see the upcoming section “Creating A **shutdown** Message” for details on how to implement it properly. You can also change the file the message should go into, if you want to.

+   21. Finally, go to:
+   
+       ```
+       passwd-check rfc822 warn
+       ```

+   22. Leave this statement alone unless this machine only runs anonymous FTP service. If this is the case, change it to:
+   
+       ```
+       passwd-check trivial enforce
+       ```
+   
+       This action ensures that **wu-ftpd** looks for email addresses—or at least the @ symbol—in the passwords it receives and will not connect a user without that information. You can better track who is coming through when you ensure that you get email addresses as the password.

+   23. Press the Esc key to enter Command mode, and then type “ZZ” to save and close the file.

+   24. Type “vi /etc/ftphosts” to open the next file.

+   25. Type “G” to go to the end of the file, and then type “o” to open a new line at the end and enter Insert mode.

+   26. Add **allow** statements if you want them. These enable you to specify who can access your FTP site through specific usernames.

> **WARNING!** *If you add any allow statements, it is assumed that you only want hosts that you define as allowed to be able to access your FTP site. You must explicitly allow everything you want to let in.*

+   27. Add **deny** statements if you want them. These enable you to specify particular locations from which people cannot access certain login names through FTP.

+   28. Press the Esc key to enter Command mode, and then type “ZZ” to save and close the file.

+   29. Type “vi /etc/ftpusers” to open the final FTP security file.