+   17. Which of the following file-location commands is likely to take the *most* time to find a file that may be located anywhere on the computer (assuming the operation succeeds)?
+       A. The **find** command.
+       B. The **locate** command.
+       C. The **whereis** command.
+       D. They're all equal in speed.

+   18. What can the **type** command do that **whereis** can't do?
+       A. Identify the command as being for **x86** or **x86-64** CPUs
+       B. Locate commands based on their intended purpose, not just by name
+       C. Identify a command as an alias, internal command, or external command
+       D. Assist in typing a command by finishing typing it for you

+   19. You want to track down all the files in **/home** that are owned by **karen**. Which of the following commands will do the job?
+       A. **find** **/home** -uid **karen**
+       B. **find** **/home** -user **karen**
+       C. **locate** **/home** -username **karen**
+       D. **locate** **/home** **karen**

+   20. What can you conclude from the following interaction?
+       $
+           $ which man
+           /usr/bin/man
+           A. The only file called man on the system is in /usr/bin.
+           B. The /usr/bin/man program was installed by system package tools.
+           C. The /usr/bin/man program will be run by any user who types man.
+           D. The first instance of the man program, in path search order, is in /usr/bin.