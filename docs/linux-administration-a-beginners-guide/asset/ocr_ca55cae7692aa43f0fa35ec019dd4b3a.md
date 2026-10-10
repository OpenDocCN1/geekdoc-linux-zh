With the accounts created, you will need to make sure the home directory for the anonymous ftp user is set up. This is the directory that users will see when connecting to the service.

# ### Setting Up the Anonymous FTP Directory

> **TIP:** If you used the anonftp-2.1-1096.rpm, RPM, you can skip these steps, too, since the directory structure has been set up for you.

The anonymous FTP directory should have the following subdirectories:

+   * pub
+   * bin
+   * etc
+   * lib

The permissions on these directories should be set with the following commands:

```
```
[root@ford /home/ftp]# chown root.root bin etc lib
[root@ford /home/ftp]# chown root.ftp pub
[root@ford /home/ftp]# chmod 111 bin etc
[root@ford /home/ftp]# chmod 755 lib
[root@ford /home/ftp]# chmod 2755 pub
```
```

When an anonymous ftp user logs in, the server performs a chroot, a system function that changes the definition of what the root directory is from whatever directory the anonymous FTP files are located in. In the case where the anonymous FTP files are located in /home/ftp, the chroot command could change the root directory definition to be /home/ftp, thus a “cd /” would really refer to /home/ftp. This is done so that any- home users cannot see other files in the system, especially sensitive ones such as /etc/passwd. The side effect of doing the chroot is that the programs that are running must be available in this new root directory, or they cannot be used. Thus, you must copy the files shown in the following table into the following directories. (Note: we assume that /home/ftp is the directory where the anonymous ftp files will be.)

| Source File | Destination | Permissions |
| :--- | :--- | :--- |
| /lib/lib-2.1.lso | /home/ftp/lib | 755 |
| /lib/libc-2.1.lso | /home/ftp/lib | 755 |
| /lib/libns1-2.1.lso | /home/ftp/lib | 755 |
| /lib/libnss_files-2.1.lso | /home/ftp/lib | 755 |
| /usr/bin/compress | /home/ftp/bin | 111 |