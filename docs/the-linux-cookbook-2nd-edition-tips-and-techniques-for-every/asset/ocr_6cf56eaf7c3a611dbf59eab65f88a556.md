+   - To find all the files on the system whose status has changed more recently than the file /etc/inittab was modified, type:
+     $ find / -cnewer /etc/inittab [RET]
+   - To find all files in the current directory tree whose status last changed exactly twenty-four hours ago, type:
+     $ find . -ctime 1 [RET]
+   - To find all files in the current directory tree whose status has changed within the last twenty-four hours, type:
+     $ find . -ctime -1 [RET]

Include the -daystart option to measure time from the beginning of the current day, instead of 24 hours ago. This option must precede the time expression it works on.

⇒ To find all files in the current directory tree whose status last changed a week ago, type:
  $ find . -daystart -ctime 7 [RET]

# 7.2.5 Finding Files in a Directory Tree by Modification Time

To find files last modified at a specified time, use find with the -mtime or -mmin options; the argument you give with -mtime specifies the number of 24-hour periods, and with -mmin it specifies the number of minutes.

⇒ Here are some ways to use this.

+   - To list all the files in the current directory tree whose contents have been modified within the last ten minutes, type:
+     $ find . -mmin -10 [RET]
+   - To list the files in the /usr/local directory tree that were modified exactly 24 hours ago, type:
+     $ find /usr/local -mtime 1 [RET]
+   - To list the files in the /usr directory tree that were modified exactly five minutes ago, type:
+     $ find /usr -mmin 5 [RET]
+   - To list the files in the /usr/local directory tree that were modified within the past 24 hours, type:
+     $ find /usr/local -mtime -1 [RET]