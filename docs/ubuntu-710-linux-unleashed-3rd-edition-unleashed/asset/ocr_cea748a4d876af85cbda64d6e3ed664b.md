# TABLE 18.2 Magic Cookies for the Shutdown File

| Cookie | Description |
| --- | --- |
| %s | The time the system will be shut down |
| %r | The time new connections will be denied |
| %d | The time current connections will be dropped |

# Configuring FTP Server File-Conversion Actions

The FTP server can convert files during transfer to compress and uncompress files automatically. Suppose that the user is transferring a file to his Microsoft Windows machine that was TARed and GZIPed on a Linux machine. If the user does not have an archive utility installed to uncompress these files, he cannot access or use the files.

As the FTP server administrator, you can configure the FTP server to automatically unarchive these files before download should the site support users who might not have unarchive capabilities. Additionally, you can configure an upload area for the users, and then configure the FTP server to automatically compress any files transferred to the server.

The structure of the format of the ftpconversions file is:

```
1:2:3:4:5:6:7:8
```

where 1 is the strip prefix, 2 is the strip postfix, 3 is the add-on prefix, 4 is the add-on postfix, 5 is the external command, 6 is the types, 7 is the options, and 8 is the description.

# Strip Prefix

The strip prefix is one or more characters at the beginning of a filename that should be automatically removed by the server when the file is requested. By specifying a given prefix to strip in a conversions rule, such as the user can request the file devel1_procmail.tar.gz by the command get procmail.tar.gz, and the FTP server performs any other rules that apply to that file and retrieve it from the server. Although this feature is documented, as of version 2.6.2, it has yet to be implemented.

# Strip Postfix

The strip postfix works much the same as the strip prefix, except that one or more characters are taken from the end of the filename. This feature is typically used to strip the .gz extension from files that have been TARed and GZIPed when the server is performing automatic decompression before sending the file to the client.