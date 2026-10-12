As the listing shows, you can start the command-line FTP client by typing the command ftp hostname, where hostname is the name of the system you want to access. When the FTP client establishes a connection with the FTP server at the remote system, the FTP server prompts you for a user name and password. After you've supplied the information, the FTP client displays the ftp> prompt, and you can begin typing commands to perform specific tasks. If you can't remember a specific FTP command, type help to view a list of them. You can get additional help for a specific command by typing help command, where command is what you want help on.

Many FTP commands are similar to the Linux commands for navigating the file system. For example, cd changes directory, pwd prints the name of the current working directory, and ls lists the contents of the current directory. Two other common commands are get and put — get is what downloads a file from the remote system to your system, and put uploads (sends) a file from your system to the remote host.

Table 4-1 describes some commonly used FTP commands. You don't have to type the entire FTP command. For a long command, you have to type the first few characters only — enough to identify the command uniquely. For example, to delete a file, you can type dele and to change the file transfer mode to binary, you can type bin.

![](bbox=[0.15, 0.55, 0.23, 0.68])

When downloading files from the Internet, you almost always want to transfer the files in binary mode because the software is usually archived and compressed in a binary form (its files aren't plain text files). So always use the binary command to set the mode to binary. Then use the get command to download the files.

Table 4-1 Commonly Used FTP Commands

| Command | Description |
|---|---|
| ! | Executes a shell command on the local system. For example, ! ls lists the contents of the current directory on the remote system. |
| ? | Displays a list of commands (same as help). |
| append | Appends a local file to a remote file. |
| ascii | Sets the file-transfer type to ASCII (or plain text). This is the default file transfer type. |
| binary | Sets the file-transfer type to binary. |
| bye | Ends the FTP session with the remote FTP server and quits the FTP client. |
| cd | Changes the directory on the remote system. For example, cd /pub/Linux changes the remote directory to /pub/Linux. |