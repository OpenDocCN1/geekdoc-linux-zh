+   - *lastlog*—This command formats and prints the contents of the last login log file (`/var/log/lastlog`). The login name, port, and last login time are displayed.
+     Entering the command without options displays the entries sorted by numerical ID.
+     You can use options such as `-u login_name` (display information for designated user only) and `-h` (display a one-line help message).
+     If a user has never logged in, the message “**Never logged in**” is displayed in place of the port and time.
+     For example, entering `lastlog` returns information similar to the following:

```
```text
dal0:~ # lastlog
Username      Port                 Latest
at                                  **Never logged in**
bin                                 **Never logged in**
...
root          pts/0                Wed May 24 10:33:36 +0200 2006
sshd                                **Never logged in**
suse-ncc                             **Never logged in**
uucp                                **Never logged in**
wwwrun                              **Never logged in**
geeko         :0                   Wed May 24 13:54:29 +0200 2006
...
```
```

# Objective 4—View and Manage Processes

To manage processes on your SUSE Linux Enterprise Desktop, you need to know the following:

+   - Understand Process Definitions
+   - Learn Jobs and Processes
+   - Manage Foreground and Background Processes
+   - View and Prioritize Processes
+   - End a Process
+   - Understand Services (Daemons)
+   - Manage a Daemon Process

# Understand Process Definitions

The following terms are used to describe Linux processes:

+   - *Program*—A structured set of commands stored in an executable file on a Linux file system. A program can be executed to create a process.
+   - *Process*—A program that is loaded into memory and executed by the CPU.
+   - *User process*—A process launched by a user that is started from a terminal or within the graphical environment.