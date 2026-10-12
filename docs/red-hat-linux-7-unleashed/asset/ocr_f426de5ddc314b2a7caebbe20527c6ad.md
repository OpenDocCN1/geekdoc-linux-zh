**smbclient** provides command-line options to query a server for the shared directories available or to exchange files. For more information on all the command-line options, consult the man page for **smbclient**. Use the following command to list all available shares on the machine `192.168.100.1`:

`$ smbclient -NL 192.168.100.1`

Any name resolving to the IP address can be substituted for the IP address. The -N parameter tells **smbclient** not to query for a password if one isn't needed, and the -L parameter requests the list.

To transfer a file, you must first connect to the Samba server using the following command:

`$ smbclient //192.168.100.1/homes -U tackett`

The parameter `//192.168.100.1/homes` specifies the remote service on the other machine. This is typically either a filesystem directory or a printer. Any name resolving to the IP address can be substituted for the IP address. The -U option enables you to specify the username you want to connect with. There are many additional **smbclient** command configurations; see the **smbclient** man page for full details. The **smbclient** utility prompts you for a password if this account requires one and then places you at this prompt:

`smb: \`

`\` indicates the current working directory.

From this command line, you can issue the commands shown in Table 17.1 to transfer and work with files.

**TABLE 17.1** **smbclient** Commands

| Command | Parameters | Description |
| :--- | :--- | :--- |
| `?` or `help` | [command] | Provides a help message on command or in general if no command is specified. |
| `!` | [shell command] | Executes the specified shell command or drops the user to a shell prompt. |
| `cd` | [directory] | Changes to the specified directory on the server machine (not the local machine). If no directory is specified, **smbclient** reports the current working directory. |