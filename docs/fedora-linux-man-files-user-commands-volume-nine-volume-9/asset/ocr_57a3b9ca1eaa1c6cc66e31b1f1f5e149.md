fail if the server does not. The client requests that the server change the UNIX user and group ownership to the given decimal values. Note there is currently no way to remotely look up the UNIX uid and gid values for a given na. This may be addressed in future versions of the CIFS UNIX extensions.

close <fileid>

Closes a file explicitly opened by the open command. Used for internal Saa testing purposes.

del <mask>

The client will request that the server attempt to delete all files matching mask from the current working directory on the server.

dir <mask>

A list of the files matching mask in the current working directory on the server will be retrieved from the server and displayed.

du <filena>

Does a directory listing and then prints out the current disk usage and free space on a share.

echo <nuer> <data>

Does an SMBecho request to ping the server. Used for internal Saa testing purposes.

exit

Terminate the connection with the server and exit from the program.

get <remote file na> [local file na]

Copy the file called remote file na from the server to the machine running the client. If specified, na, the local copy local file na. Note that all transfers in sclent are binary. See also the lowercase command.

getfacl <filena>

Requires the server support the UNIX extensions. Requests and prints the POSIX ACL on a file.

hardlink <src> <dest>

Creates a hardlink on the server using Windows CIFS semantics.