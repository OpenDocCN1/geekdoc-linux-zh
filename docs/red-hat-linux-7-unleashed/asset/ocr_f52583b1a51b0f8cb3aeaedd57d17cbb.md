# **Table 17.1** continued

| Command | Parameters | Description |
| --- | --- | --- |
| lcd | [directory] | Changes to the specified directory on the local machine. If no directory is specified, smbcient will report the current working directory on the local machine. |
| del | [files] | The specified files on the server are deleted if the user has permission to do so. Files can include wildcard characters. |
| dir or ls | [files] | Lists the indicated files. You can also use the command ls to get a list of files. |
| exit or quit | none | Exits from the smbcient program. |
| get | [remotefile] [local name] | Retrieves the specified remotefile and saves the file on the local server. If local name is specified, the copied file will be saved with this filename rather than the filename on the remote server. |
| mget | [files] | Copies all the indicated files, including those matching any wildcards, to the local machine. |
| md or mkdir | [directory] | Creates the specified directory on the remote machine. |
| rd or rmdir | [directory] | Removes the specified directory on the remote machine. |
| put | [localfile] [remotename] | Copies the specified file from the local machine to the server. |
| mput | [files] | Copies all the specified files from the local machine to the server. |
| print | [file] | Prints the specified file on the remote machine. |
| queue | none | Displays all the print jobs queued on the remote server. |

You can specify the password on the command line by appending a percent sign to the username followed by the password:

```
`$ smbcient //192.168.100.1/homes -U tackett%tackettspasswrd`
```

Although the preceding command is convenient, many versions of UNIX show the password portion of the command in clear text in a ps command. Default Red Hat Linux 7 installations show the password as a string of x characters, but in security-critical environments, or where someone might be looking over your shoulder, it’s better to let smbcient prompt for the password and accept it silently.