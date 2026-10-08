ARPA is a combination of “ARPA Services” and “Berkeley Services.” ARPA Services supports communications among systems running different operating systems, and Berkeley Services supports UNIX systems. The following sections are a list of the most common commands. Although many programs can be run under each of these services, the following are the most commonly used ones in the UNIX world. In some cases, there are examples that show how these commands are used. For most of the examples, the local host is system1 and the remote host is system2.

# ## ARPA Services (Communication among Systems w/ Different OS)

![](bbox=[0.03, 0.39, 0.12, 0.45])

**File Transfer Protocol (ftp)**  Transfer a file, or multiple files, from one system to another. This is often used when transferring files between a UNIX workstation and a Windows PC, VAX, etc. The following example shows copying the file /tmp/krsort.c from system2 (remote host) to the local directory on system1 (local host):

| Command Sequence | comments |
| :--- | :--- |
| `$ ftp system2` | Issue ftp command |
| Connected to system2. | |
| system2 FTP server (Version 4.1) ready. | |
| Name (system2:root): root | Log in to system2 |
| Password required for root. | |
| Password: | Enter password |
| User root logged in. | |
| Remote system type is UNIX. | |
| Using binary mode to transfer files. | |
| `ftp> cd /tmp` | cd to /tmp on system2 |
| CWD command successful | |
| `ftp> get krsort.c` | Get krsort.c file |
| PORT command successful | |
| Opening BINARY mode data connection for krsort.c | |
| Transfer complete. | |
| 2896 bytes received in 0.08 seconds | |