# COMMANDS (CONT.)

# Use This Option

append *local filename* [ *remote filename* ]

ascii

bell

binary

bye

case

cd *directory*

cdup

chmod *mode filename*

close

cr

delete *filename*

dir [ *directory* | *filename* ]

disconnect

# To Do This

Append the specified local filename to a file on the remote machine. If you do not specify a remote filename, a file is created on the remote machine with the same name as the local filename, but characters and line termination settings are changed according to the remote machine’s settings, if any.

Set the file transfer type to ASCII. This is the default.

Sound the bell after each file is successfully transferred.

Set the file transfer type to binary.

Close the FTP session and quit the **ftp** utility.

Toggle case mapping on or off. Case mapping is off by default. When case mapping is on, remote uppercase filenames are written to the local system in lowercase letters.

Change to the specified directory.

Change to the parent directory.

Change the permissions of the remote filename to the specified mode.

Terminate the FTP session with the remote server but without quitting the **ftp** utility. See also **bye** in this table.

Toggle ASCII-mode carriage return stripping on and off. The default is on.

Delete the specified filename on the remote machine.

Display the contents of the directory. Optionally, save to the specified filename.

Terminate the FTP session with the remote server but without quitting the **ftp** utility. Same as **close**. See also **bye**.