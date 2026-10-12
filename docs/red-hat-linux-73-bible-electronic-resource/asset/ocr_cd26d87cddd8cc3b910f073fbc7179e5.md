Depending on how the FTP server is configured, you may or may not be able to do some of the file and directory commands shown above. In general, if you log in as the anonymous user, you will not be able to modify any files or directories. You will only be able to download files. If you have a real login account, you will typically have the same read and write permission you have when you enter the computer using a standard login prompt.

# FTP file copying commands

Before you copy files between the remote and local systems, consider the type of transfer you want to do. The two types of transfer modes are:

+   - binary — For transferring binary files (such as data files and executable commands). This is also referred to as an image transfer.
+   - ascii — For transferring plain-text files.

The Linux ftp command seems to set the default to binary when you start FTP. Binary seems to work well for either binary or text files. However, binary transfers may not work transferring ascii files from non-UNIX systems. If you transfer an executable file in ascii mode, the file may not work when you try to run it on your local system.

Most file copying is done with the get and put commands. Likewise, you can use the mget and mput commands to transfer multiple files at once. Some FTP servers will even allow you to use matching characters (for example, `get abc*` to get all files beginning with the letters abc). Here are descriptions of those commands:

+   - get file — Copies a file from the current directory on the remote file system and copies it to the current directory on the local file system. You can use a full path along with the filename. You can also specify the path to the local file where the remote file will be placed. Here are some examples:

```
get route
get /tmp/options /home/mike/op
get /tmp/sting
```

The first example takes the file `route` from the current remote directory and copies it to the current local directory. The second example copies the remote file `/tmp/options` and copies it to the local file `/home/mike/op`. The third example copies the file `/tmp/sting` from the remote system to the file `tmp/sting` relative to the current directory on the local system. So if your current directory were `/home/jake`, ftp would try to copy the file to `/home/jake/tmp/sting`.

+   - put file — Copies a file from the current local directory to the current remote directory. The usage of this command is essentially the same as the `get` command, except that files are copied from the local to the remote system.

> NOTE: Anonymous FTP sites (described later) usually let you copy files *from* them, but not to them. If they do allow you to put files on their server, it will usually be in a restricted area.