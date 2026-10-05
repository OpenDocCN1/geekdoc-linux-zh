# Networking and Internet Services
PART II

\ indicates the current working directory.

From this command line, you can issue the commands shown in Table 16.1 to transfer and
work with files.

# Table 16.1 smbClient Commands

| Command Parameters | Description |
|---|---|---|
| ? or help | [command] | Provides a help message on command or in general if no command is specified. |
| ! | [shell command] | Executes the specified shell command or drops the user to a shell prompt. |
| cd | [directory] | Changes to the specified directory on the server machine (not the local machine). If no directory is specified, smbclient reports the current working directory. |
| lcd | [directory] | Changes to the specified directory on the local machine. If no directory is specified, smbclient will report the current working directory on the local machine. |
| del | [files] | The specified files on the server are deleted if you has permission to do so. Files can include wildcard characters. |
| dir or ls | [files] | Lists the indicated files. You can also use the command ls to get a list of files. |
| exit or quit | none | Exits from the smbclient program. |
| get | [remotefile] [local name] | Retrieves the specified remotefile and saves the file on the local server. If *local name* is specified, the copied file will be saved with this filename rather than the filename on the remote server. |
| mget | [files] | Copies all the indicated files, including those matching any wildcards, to the local. If recursion is typed prior to this command, the contents of all directories specified will be copied as well. |
| md or mkdir | [directory] | Creates the specified directory on the remote machine. |
| rd or rmdir | [directory] | Removes the specified directory on the remote machine. |
| put | [localfile] [remotename] | Copies the specified file from the local machine to the server. |
| mput | [files] | Copies all the specified files from the local machine to the server. If recursion is typed prior to this command, the contents of all directories specified will be copied as well. |
| print | [file] | Prints the specified file on the remote machine. |
| queue | none | Displays all the print jobs queued on the remote server. |

*? *