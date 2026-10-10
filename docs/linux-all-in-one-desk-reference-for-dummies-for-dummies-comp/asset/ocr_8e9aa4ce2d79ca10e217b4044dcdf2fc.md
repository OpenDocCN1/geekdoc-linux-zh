# Table 4-1 (continued)

| Command | Description |
|---|---|
| **mkdir** | Creates a directory on the remote system. `mkdir images` creates a directory named `images` in the current directory on the remote system. |
| **mIs** | Same as **mdir** |
| **mput** | Uploads multiple files. For example, `mput *.jpg` sends all files with names ending in `.jpg` to the remote system. If the prompt is turned on, the FTP client asks for confirmation before sending each file. |
| **open** | Opens a connection to the FTP server on the specified host. For example, `open ftp.netscape.com` connects to the FTP server on the host `ftp.netscape.com`. |
| **prompt** | Turns the prompt on or off. When the prompt is on, the FTP client prompts you for confirmation before downloading or uploading each file during a multiple-file transfer. |
| **put** | Sends a file to the remote system. For example, `put index.html` sends the `index.html` file from the local system to the remote system. |
| **pwd** | Displays the full path name of the current directory on the remote system. When you log in as a user, the initial current working directory is your home directory. |
| **quit** | Same as **bye** |
| **recv** | Same as **get** |
| **rename** | Renames a file on the remote system. For example, `rename old.html new.html` renames the file `old.html` to `new.html` on the remote system. |
| **rmdir** | Deletes a directory on the remote system. For example, `rmdir images` deletes the `images` directory in the current directory of the remote system. |
| **send** | Same as **put** |
| **size** | Shows the size of a remote file. For example, `size bigfile.tar.gz` shows the size of that remote file. |
| **status** | Shows the current status of the FTP client |
| **user** | Sends new user information to the FTP server. For example, `user naba` sends the username `naba`; the FTP server then prompts for the password for that username. |