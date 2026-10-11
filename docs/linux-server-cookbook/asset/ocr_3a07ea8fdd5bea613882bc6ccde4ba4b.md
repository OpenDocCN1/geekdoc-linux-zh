+   • Character—indicates that it is a regular file.
+   • Letter d indicates that it is a directory.
+   • Letter l indicates that it is a symbolic link.
+   • Letter c indicates that it is a character device
+   • Letter p indicates that it is a pipe
+   • Letter s indicates that it is a socket
+   • Letter d indicates that it is a block device.

After the file type, the next three characters indicate the permissions for the user owner, then the next three for the group owner, and the last three for other users. *Figure 5.2* shows some examples of different permissions and file types:

```
root@ubuntu:~# ls -ld /etc/{,passwd,shadow} /dev/{vda,console} /run/snapd.socket
crw-rw---- 1 root tty 5, 1 Jul 25 17:40 /dev/console
brw-rw---- 1 root disk 252, 0 Jul 25 17:40 /dev/vda
drwxr-xr-x 97 root root 4096 Jul 24 15:31 /etc/
-rw-r--r-- 1 root root 1838 Jul 24 13:32 /etc/passwd
-rw-r----- 1 root shadow 1198 Jul 24 13:32 /etc/shadow
srw-rw-rw- 1 root root 0 Jul 25 17:40 /run/snapd.socket
```

*Figure 5.2: Different types of files and permissions associated.*

The third column indicates the user owner, and the fourth indicates the group owner. For example, for the file /etc/shadow in the figure, the user root has read and write access to the file, and the members in the group shadow have read-only access. The rest of the users have no access to the file for security reasons, as this file contains encrypted passwords.

Another way to see the permissions for a file or directory is by using the command *stat*, which will show more related information, such as when the file was modified, changed (permissions or owners), created, or accessed. *Figure 5.3* shows an example using the file /etc/passwd:

```
root@ubuntu:~# stat /etc/passwd
File: /etc/passwd
Size: 1838 Blocks: 8 IO Block: 4096 regular file
Device: fd00h/64768d Inode: 397042 Links: 1
Access: (0644/-rw-r--r--) Uid: ( 0/root) Gid: ( 0/root)
Access: 2022-07-30 09:55:03.691999361 +0000
Modify: 2022-07-24 13:32:07.456812114 +0000
Change: 2022-07-24 13:32:07.456812114 +0000
Birth: 2022-07-24 13:32:07.45681214 +0000
```

*Figure 5.3: Output example for command stat.*