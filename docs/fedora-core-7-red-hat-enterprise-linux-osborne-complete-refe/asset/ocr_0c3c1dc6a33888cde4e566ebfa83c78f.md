# **Ownership**

Files and directories belong to both an owner and a group. A group usually consists of a collection of users, all belonging to the same group. In the following example, the **mydata** file is owned by the user **robert** and belongs to the group **weather**:

```
```text
-rw-r--r-- 1 robert weather 207 Feb 20 11:55 mydata
```
```

A group can also consist of one user, however, normally the user who creates the file. Each user on the system, including the root user, is assigned their own group, of which they are the only member, ensuring access only by that user. In the next example, the report file is owned by the **robert** user and belongs to that user’s single user group, **robert**:

```
```text
-rw-r--r-- 1 robert robert 305 Mar 17 12:01 report
```
```

The root user, the system administrator, owns most of the system files that also belong to the root group, of which only the root user is a member. Most administration files, like configuration files in the */etc* directory, are owned by the root user and belong to the root group. Only the root user has permission to modify them, whereas normal users can read and, in the case of programs, also execute them. In the next example, the root user owns the *fstab* file in the */etc* directory, which also belongs to the root user group:

```
```text
-rw-r--r-- 1 root root 621 Apr 22 11:03 fstab
```
```

Certain directories and files located in the system directories are owned by a service, rather than the root user, because the services need to change those files directly. This is particularly true for services that interact with remote users, such as Internet servers. Most of these files are located in the */var* directory. Here you will find files and directories managed by services like the Squid proxy server and the Domain Name Server (named). In this example, the Squid proxy server directory is owned by the **squid** user and belongs to the **squid** group:

```
```text
drwxr-x--- 2 squid squid 4096 Jan 24 16:29 squid
```
```

# **Changing a File's Owner or Group: chown and chgrp**

Although other users may be able to access a file, only the owner can change its permissions. If, however, you want to give some other user control over one of your file's permissions, you can change the owner of the file from yourself to the other user. The **chown** command transfers control over a file to another user. This command takes as its first argument the name of the other user. Following the username, you list the files you are transferring. In the next example, the user gives control of the **mydata** file to user **robert**:

```
```text
$ chown robert mydata
$ ls -1 mydata
-rw-r--r-- 1 robert weather 207 Feb 20 11:55 mydata
```
```

You can also, if you wish, change the group for a file, using the **chgrp** command. **chgrp** takes as its first argument the name of the new group for a file or files. Following the new group name, you list the files you want changed to that group. In the next example, the