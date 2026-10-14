You can use the write command only when the recipient is logged in. Use the who command, as described in Section 10.1, to list current users. If, for example, user smith is not logged on when you send a message through write, the following message is displayed on your terminal screen:

smith is not logged on

The following steps show how user wang sends a message to user chung, both of whom are logged in on local host dancer:

+   1. User wang enters the write command at the system prompt:
+   
+   dancer$ write chung
+   
+   The write program rings a bell and sends the following message to the terminal screen of chung:
+   
+   message from wang tty04 Feb 14 10:32:45
+   
+   A bell rings user wang’s terminal when the connection is made.

+   2. User wang types the message, pressing the Return key after each line, and ends the message by pressing Ctrl/D. For example, wang sends the following message in two lines to user chung:
+   
+   The double-sided lab printer is working. Return
+   Re-send your job, and I’ll check it. Return
+   Ctrl/D

+   3. After wang presses Ctrl/D, the EOF (end of file) signal is displayed on the screen of user chung to indicate the end of the message.

Note
See your system administrator if pressing Ctrl/D does not produce the EOF signal on the recipient’s screen or if a bell does not ring on the sender’s terminal.

You can use the exclamation point (!) at the beginning of a new message line to access the shell prompt and execute any operating system command (including write). For example, if wang forgot the name of the current directory from which chung is to retrieve certain files, wang can enter the !pwd command to remind himself, as shown:

```
dancer$ write chung
You can copy the network user files from: Return
!pwd Return
/ufs/usr/staff/r0/net-dir/network_comm
!
/ufs/usr/staff/r0/net-dir/network_comm
Ctrl/D
dancer$
```