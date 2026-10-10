
## UPLOAD

You can use the `upload` command, along with `path-filter`, to control files placed onto your server. The `upload` command specifies the permissions that the client has to place files in certain directories, as well as the permissions the files will take on after they are placed there. The format of the command is

```
upload directory dirglob switch owner group perms mkdir
```

where `directory` is the directory that is affected by this command, `dirglob` is the regular expression used to determine whether a subdirectory under `directory` is a valid place to create an upload, and `switch` is either YES or NO, thereby establishing whether an upload can happen in `directory`. The `owner`, `group`, and `perms` parameters establish just that—the file's owner, group, and permissions. Finally, you can specify the `mkdir` operation as either DIRS or NODIRS, determining whether the client can create subdirectories under the specified `directory`. For example:

```
upload /home/ftp /incoming yes ftp ftp 0400 nodirs
```

> NOTE: The upload command affects only the directory listed, not any subdirectories beneath it. This prevents remote users from being able to create arbitrary directories on your server and hiding files in there.

## The Log File

As we discussed earlier, the log file is important in your day-to-day operations. With it, you can perform an analysis of your TFTP site and determine things like what the most commonly accessed files are and usage patterns for the site as a whole.

The default location for the TFTP log file is `/var/log/xferlog`. Each line of the log contains the entry shown in Table 13-1.

| Log Title Entry | Description |
|---|---|
| **Current-time** | The time at which the entry occurred. The format of this is DDD MMM dd hh:mm:ss YYYY, where DDD is the day of the week, MMM is the month, dd is the day of the month, hh:mm:ss is the time in hours, minutes, and seconds, and YYYY is the year. |
| **Transfer-time** | The number of seconds it took to perform the transfer of this particular entry. |
| **Remote-host** | The client’s host name. |
| **File-size** | Size of the file being transferred. |
| **File-name** | Name of the file being transferred. |
| **Transfer-type** | Either a for ASCII or b for binary. |
| **Special-action-flag** | A list of actions performed on the file by the server: A means the file was compressed, U means the file was tarred, and a hyphen (-) means that no action was taken. |
| **Direction** | The direction of the transfer, where o means outbound and i means inbound. |
| **Access-mode** | The type of user that performed the transaction: a for anonymous, r for real, and g for guest. |
| **Username** | The local user name if the User-type is set to real. |
| **Service-name** | The name by which the FTP server was invoked. |
| **Authentication-method** | The type of authentication done by the server on the user. 0 means no authentication was done, 1 means the user had to log in with a unique login/password combination. |
| **Authenticated-user-id** | If the user had to log in with a unique login/password combination, the login would be here. Anonymous transfers are listed as anonymous. |

## File Conversions on the Fly

Sometimes, clients will not have the necessary tools to make use of the file they are downloading, because it is either compressed or archived in a format that they cannot read. (This used to especially be true with tar.gz files until WinZip started unarchiving those files as well.) Other times the reverse is true: the client is able to handle compressed files and would prefer receiving the file in a compressed format. Of course, file compression is just one of infinite types of use that you can set up with an `ifc/ftpfileconversions` file. The format of the file is

```
stripips:stripos:addnopp:addnopost:external:type:options:desc
```

The fields are as shown in Table 13-2.

## A Sample Entry

The following is a sample entry that compresses files using gzip on demand. This would allow someone who wants to get the file `opt_1_disccography.tar` to instead request the file `orb_discography.tar.gz` and have the server compress the file using gzip before sending it to him. The configuration line that does this is as follows:

```
:::gz::bin/gzip -9 -c %s::”RG[!T_ASCII]::O_COMPRESS::GZIP
```

| Field | Description |
| :--- | :--- |
| **Stripoff** | The strip prefix is the starting characters of a filename that are removed before the file is transferred. For example, if the strip prefix is set to “weding,” And a full filename is “weding.ring,” a user could simply request a file “ring” and wu-ftpd would know which file to get as well as what kind of conversion to do with it. |
| **Strippost** | The strip postfix is the same as the strip prefix, except it is for the end of the file instead. For example, if the strip postfix is set to “.gz” and a filename on the server is “ring.gz,” the server would know to perform the action matching this line in the configuration file if the client requested the file “ring.” |
| **Addonpost** | Add-on postfix is the opposite of stripoff in that instead of removing the end of a filename, it appends to it. This would be used in a case where a file that isn’t compressed gets .gz added to it as it is compressed and sent to the client. |
| **Addonpre** | Add-on prefix is the opposite of stripre. It allows you to add a prefix to a filename before it is sent to a client. |
| **External** | This entry specifies which program (external to wu-ftpd) is run when a filter matches. In the case of downloads, the resulting file after conversion should be sent to a program’s standard output (stdout). Uploads are sent to the program’s standard in (stdin). You can specify the filename the client requested in the command line for the external command by using %s instead of the name itself. The server will automatically search and replace every occurrence of %s with the client’s filename. |
| **Type** | In the world of wu-ftpd, files exist as one of three types: regular, ASCII, and directories (T_REG, T_ASCII, and T_DIR, respectively). This field allows you to specify the type of file that wu-ftpd should act on if the filename filter matches. You can specify multiple options by separating them with a pipe symbol (\|). For example, T_REG\|T_ASCII specifies that you want the filter to be applied to any type of file. |

**Table 13-2. Fields of the /etc/ftpconversions File**

| Field | Description |
| --- | --- |
| **Options** | This field decides whether this filter is going to compress, uncompress, or tar files. Each option is represented by O_COMPRESS, O_UNCOMPRESS, and O_TAR, respectively. You can do multiple things to a file at once by using the pipe (I) symbol between commands. For example, O_COMPRESS|O_TAR means that this filter will both compress and tar a client request. |
| **Desc** | This is a freeform field that allows you to describe what the filter does. |

**Table 13-2 Fields of the /etc/tftp/conversions File (continued)**

The first two parameters (strip prefix and strip postfix) are not necessary since we are not taking anything away from the filename. The third parameter (add-on prefix) doesn’t apply since we do not want to add anything to the beginning of the filename. The fourth parameter, gz (add-on postfix), specifies that the filename should have .gz appended to it after this filter is done executing. The fifth parameter (external command) specifies the exact invocation of the gzip program in order to perform the file compression. Notice that %s is used instead of a filename. The sixth parameter (type of file) tells wu-ftpd that it can perform compression on both straight ASCII as well as regular files. The seventh parameter, O_COMPRESS (the options field), tells the server that the file action being performed is compression. Finally, the last field is a simple human readable reminder of what this filter does: run gzip.

Although this appears intimidating, don’t worry about it! It is unlikely you’ll need to change the default configuration file that comes with wu-ftpd since it covers the most popular conversions.

## Configuring Host Access

The /etc/ftphosts file allows you to explicitly allow or deny users based on their originating IP address. Each line in the file can take the form

```
allow username address
```

or

```
deny username address
```

Where username is the login they use when connecting to the FTP service, and address is the originating IP address. You can list multiple addresses in a comma-separated list.
