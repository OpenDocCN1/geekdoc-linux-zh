
## Allow Users to Rename Files

You can enable or prevent a user from renaming files by using this command line:

```
rename <yes|no> <typelist>
```

The yes|no parameter toggles the permission on or off, and typelist is the same comma-delimited string as seen in chmod.

## Allow Users to Compress Files

This line determines whether the user is able to use the compress command on files:

```
compress <yes|no> [<classglob>]
```

The yes|no parameter toggles the permission on or off, and classglob is a regular expression string that specifies one or more defined classes of users. The conversions that result from the use of this command are specified in the ftpconversions file, which contains directions on what compression or extraction command is to be used on a file with a specific extension, such as .Z for the compress command, .gz for the gunzip command, and so on. See the section “Configuring FTP Server File-Conversion Actions” later in this chapter.

## Assign or Deny Permission to Use tar

This line determines whether the user is able to use the tar (tape archive) command on files:

```
tar <yes|no> [<classglob> ...]
```

The yes|no parameter toggles the permission on or off, and classglob is a regular expression string that specifies one or more defined classes of users. Again, the conversions that result from the use of this command are specified in the ftpconversions file.

## Determine What Permissions Can Apply to User-Created Upload Files

This line is a bit different from the other commands in the permission control section. The umask command determines with what permissions a user can create new files; here it is.

```
umask <yes|no> <typelist>
```

The yes|no parameter toggles based on whether a user is allowed to create a file with his default permissions when uploading a file. Like the overwrite command you read about earlier in this section, this command line is specific to uploaded files because the client machine determines how new files are created from a download.

## Configure Commands Directed Toward the cdpath

This alias command allows the administrator to provide another name for a directory other than its standard name:

```
alias <string> <dir>
```

## TABLE 18.2 Magic Cookies for the Shutdown File

| Cookie | Description |
| --- | --- |
| %s | The time the system will be shut down |
| %r | The time new connections will be denied |
| %d | The time current connections will be dropped |

## Configuring FTP Server File-Conversion Actions

The FTP server can convert files during transfer to compress and uncompress files automatically. Suppose that the user is transferring a file to his Microsoft Windows machine that was TARed and GZIPed on a Linux machine. If the user does not have an archive utility installed to uncompress these files, he cannot access or use the files.

As the FTP server administrator, you can configure the FTP server to automatically unarchive these files before download should the site support users who might not have unarchive capabilities. Additionally, you can configure an upload area for the users, and then configure the FTP server to automatically compress any files transferred to the server.

The structure of the format of the ftpconversions file is:

```
1:2:3:4:5:6:7:8
```

where 1 is the strip prefix, 2 is the strip postfix, 3 is the add-on prefix, 4 is the add-on postfix, 5 is the external command, 6 is the types, 7 is the options, and 8 is the description.

## Strip Prefix

The strip prefix is one or more characters at the beginning of a filename that should be automatically removed by the server when the file is requested. By specifying a given prefix to strip in a conversions rule, such as the user can request the file devel1_procmail.tar.gz by the command get procmail.tar.gz, and the FTP server performs any other rules that apply to that file and retrieve it from the server. Although this feature is documented, as of version 2.6.2, it has yet to be implemented.

## Strip Postfix

The strip postfix works much the same as the strip prefix, except that one or more characters are taken from the end of the filename. This feature is typically used to strip the .gz extension from files that have been TARed and GZIPed when the server is performing automatic decompression before sending the file to the client.
