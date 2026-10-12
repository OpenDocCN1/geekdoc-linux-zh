If you want to make changes to any of the remote files or directories, use the following commands:

+   - **mkdir** — Creates a directory on the remote system.
+   
+   - **rename** — Renames a file or directory on the remote system.
+   
+   - **rmdir** — Removes a remote directory.
+   
+   - **delete** — Removes a remote file.
+   
+   - **mdelete** — Removes multiple remote files.

Depending on how the FTP server is configured, you may or may not be able to do some of the file and directory commands shown above. In general, if you log in as the anonymous user, you will not be able to modify any files or directories. You will only be able to download files. If you have a real login account, you will typically have the same read and write permission you have when you enter the computer using a standard login prompt.

# FTP file copying commands

Before you copy files between the remote and local systems, consider the type of transfer you want to do. The two types of transfer modes are:

+   - **binary** — For transferring binary files (such as data files and executable commands). This is also referred to as an image transfer.
+   
+   - **ascii** — For transferring plain-text files.

The Linux `ftp` command seems to set the default to binary when you start FTP. Binary seems to work well for either binary or text files. However, binary transfers may not work transferring ascii files from non-UNIX systems. If you transfer an executable file in ascii mode, the file may not work when you try to run it on your local system.

Most file copying is done with the `get` and `put` commands. Likewise, you can use the `mget` and `mput` commands to transfer multiple files at once. Some FTP servers will even allow you to use matching characters (for example, `get abc*` to get all files beginning with the letters abc). Here are descriptions of those commands:

+   - **get file** — Copies a file from the current directory on the remote file system and copies it to the current directory on the local file system. You can use a full path along with the filename. Here are some examples:

```
ftp> get route
ftp> get /tmp/sting
```

The first example takes the file *route* from the current remote directory and copies it to the current local directory. The second example copies the file */tmp/sting* from the remote system to the file *tmp/sting* relative to the current directory on the local