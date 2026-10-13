The message file specified will be displayed at the time the directive indicates. Two possible times can be used: `LOGIN` or `CWD=directory` where the directory is the directory which triggers the display of the message; you can specify all directories with an asterisk. In the case of the `LOGIN` time, the message file indicates the file path to the file to display but in the case of the `CWD` time, the file specified is relative to the directory being changed to. The class field is optional and is used to specify the class of users (such as anonymous, real, or group) for which the message should be displayed.

In our example, any file with a name beginning with README in a directory will be considered the readme file for the directory.

**LINE 16**  The log transfers directive is used to indicate which types of transfer should be logged to the log file (usually `/var/log/xferlog`). The directive takes the following form:

```
log transfers<$class><direction>
```

The class indicates which classes of users should have their transfers logged and the direction indicates which type of transfers to log. Possible transfer directions are inbound or outbound. You can specify both directions by separating them with a comma: `inbound,outbound`.

In our example, inbound and outbound transfers by anonymous and real users will be logged.

**LINE 17**  The shutdown directive points to a file that indicates when a shutdown will occur as well as a warning message to display to users prior to the shutdown. Generally, this file will be created with the `ftpshut` program which is discussed later this chapter in the section “Other WU-FTPd Programs.”

# **USING THE _ftpconversions_ FILE**

The `ftpconversions` file is used to tell WU-FTPd to perform on-the-fly compression and archiving using `tar`, `compress`, or `gzip` during file transfer.

The file consists of multiple entries. Each entry appears on a separate line and takes the form:

```
<strip prefix>:<strip postfix>:<addon postfix>:
➜ <external command>:<types>:<options>:<description>
```

The strip prefix and addon prefix are currently not used by WU-FTPd and are in place for future use.

The strip postfix indicates that files with the indicated ending should be passed through the specified external command and the extension removed. By contrast, the addon postfix indicates the extension to add a file when compressed with a particular external command.

The external command indicates how to perform the specific compression or decompression. In the command, `%s` is a symbol used to indicate the place where WU-FTPd should insert the filename in the command.

The types field indicates which types of files are affected by the entry. For instance, `T_ASCII` indicates that the entry applies to ASCII files. Multiple types are separated by vertical bars as