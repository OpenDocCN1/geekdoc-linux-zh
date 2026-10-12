You can use *magic cookies* to breathe life into your displayed messages. *Magic cookies* are symbolic constants that are replaced by system information. Table 24.1 lists the message command's valid magic cookies and their representations.

# TABLE 24.1 Magic Cookies and Their Descriptions

| Cookie | Description |
| :--- | :--- |
| *F | Local time (form Thu Nov 15 17:12:42 1990) |
| *F | Free space in partition of CWD (kilobytes) [Not supported on all systems] |
| *C | Current working directory |
| *E | Maintainer's email address as defined in ftpassess |
| *P | Remote hostname |
| *N | Local hostname |
| *u | Username as determined via RFC931 authentication |
| *J | Username given at login time |
| *M | Maximum allowed number of users in this class |
| *Q | Current number of users in this class |
| *B | Absolute limit on disk blocks allocated |
| *b | Preferred limit on disk blocks |
| *0 | Current block count |
| *I | Maximum number of allocated inodes (+1) |
| *i | Preferred inode limit |
| *n | Current number of allocated inodes |
| *t | Time limit for excessive disk use |
| *N | Time limit for excessive files |
| R | Uploaded bytes |
| **L | Downloaded bytes |
| *xR | Upload/download ratio (1:n) |
| %xR | Credit bytes |
| *%X | Time limit (minutes) |
| *xE | Elapsed time since login (minutes) |
| %XL | Time left |
| *xu | Upload limit |
| *xO | Download limit |

To understand how this command works, imagine that you want to display a welcome message to everyone who logs in to the FTP server. An entry of

```
```text
message /home/ftp/welcome.msg login
message /welcome.msg           login
```
```

shows the contents of the welcome.msg file to all real users who log in to the server. The second entry shows the same message to the anonymous user.