incoming directory were owned by root, 700 permission would not allow the anonymous user to upload, but 777 permission would.

# Preventing files or directories from being retrieved

Using the **noretrieve** parameter, you can prevent files with specific names or from specific directories from being retrieved. Here are some examples:

```
noretrieve relative class=world /pub.homestuff
noretrieve absolute /etc/hosts /etc/inittab
noretrieve core personal money
```

In these examples, *relative* and *absolute* keywords indicate whether the files and directories indicated are relative to the FTP user's directory (for example, /var/ftp) or an absolute path from the system's root directory. The first line indicates that any users in the class *world* cannot retrieve files from the /pub/homestuff directory relative to the /var/ftp directory (that is, /var/ftp/pub/homestuff). The second line says that the system's /etc/hosts and /etc/inittab files cannot be retrieved. When no path name is indicated, as in the third line, no files that match the names shown can be downloaded, regardless of where they reside in the file system.

# Allowing files or directories to be retrieved

If you have prevented a group of files from being retrieved using the **noretrieve** parameter, you can selectively allow certain files and directories to be retrieved using the **all-retrieve** parameter. Here's an example:

```
all-retrieve relative class=world /pub/homestuff/publicfile.txt
```

Although you restricted download from the /pub/homestuff directory in a previous example, you now allow the download of /pub/homestuff/publicfile.txt to the *world* class of users.

# Allowing permission capabilities

Even after you have allowed a user or class of users permission to upload files to your FTP server, you still have a lot of control over different aspects of writing and changing files. Each of these permission capabilities can be turned on or off for *anonymous*, *guest*, or *real* users. Or you can turn them on or off for a specific class of users. Below are a few examples. By default, all these services are turned on when a user has upload capabilities (that is, the capability to write to an FTP server).

> **NOTE:** Remember that Red Hat Linux ownership permission still applies to files and directories, regardless of how these permission capabilities are set. For example, even if you are allowed to use `chmod`, you still couldn't use it to change permission on someone else's file that was set to 0600.