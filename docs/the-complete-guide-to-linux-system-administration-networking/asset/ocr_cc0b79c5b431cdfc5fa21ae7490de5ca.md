8. A file-browsing window appears allowing you to select the directory in which you want your new archive file created and to enter a name for that archive file. Your home directory is shown by default, which is fine for this project. In the Location field of the Create New Archive – Ark window, enter testark.tgz. Then click Save. The files you dragged and dropped are listed in the Ark main window. The title bar also changes to show the name of the archive you created, testark.tgz.

9. In the Ark window, open the Action menu and click Add Folder.

10. Use the directory browser in that window (or enter in the text field below the directory browser) to select the directory /usr/share/dict, then click OK. All the files from that directory are added to the testark.tgz file and are also listed on the screen.

11. Right-click any file name in the Ark main window. What options are available for any file in the archive?

12. Choose File, then Quit from the menu of Ark. If prompted to select Save, Discard, or Cancel, click Save.

13. Delete the archive file you created by entering this command at the command line:
```
rm ~/testark.tgz
```

14. Confirm the deletion if prompted, then close the command-line window and log out.

![](bbox=[0.07, 0.68, 0.15, 0.8])

# Project 13-2

In this project, you watch the system log file as new messages are written to it by the syslogd daemon. To complete this project you need a Linux system with a graphical interface and root access.

+   1. Log in to Linux and open two command-line windows.
+   2. In each of the command-line windows, use su - to change to root access.
+   3. In one command-line window, enter this command to display the last 15 lines of the system log file, updating the display every few seconds
+   ```
+   tail -f /var/log/messages
+   ```
+   4. In the second command-line window, enter this command to restart the syslogd daemon:
+   ```
+   killall -HUP syslogd
+   ```
+   Notice that a message is added to the first window stating that the syslogd program was restarted.
+   5. In the second window, enter killall -HUP cron to restart the scheduling daemons. Were any messages added?