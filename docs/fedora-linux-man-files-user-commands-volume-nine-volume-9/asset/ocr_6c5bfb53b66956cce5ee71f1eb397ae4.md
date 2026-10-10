# logoff

Logs the user off the server, closing the session. Used for internal Saa testing purposes.

# lowercase

Toggle lowercasing of filenames for the get and mget commands.

When lowercasing is toggled ON, local filenames are converted to lowercase when using the get and mget commands. This is often useful when copying (say) MSDOS files from a server, because lowercase filenames are the norm on UNIX systems.

# ls <mask>

See the dir command above.

# mask <mask>

This command allows the user to set up a mask which will be used during recursive operation of the mget and mput commands.

The masks specified to the mget and mput commands act as filters for directories rather than files when recursion is toggled ON.

The mask specified with the mask command is necessary to filter files within those directories. For example, if the mask specified in an mget command is "source*" and the mask specified with the mask command is "*.c" and recursion is toggled ON, the mget command will retrieve all files matching "*.c" in all directories below and including all directories matching "source*" in the current working directory.

Note that the value for mask defaults to blank (equivalent to "*") and remains so until the mask command is used to change it. It retains the most recently specified value indefinitely. To avoid unexpected results it would be wise to change the value of mask back to "*" after using the mget or mput commands.

# md <directory na>

See the mkdir command.

# mget <mask>

Copy all files matching *mask* from the server to the machine running the client.

Note that *mask* is interpreted differently during recursive operation and non-recursive operation - refer to the recurse and mask commands for more information. Note that all transfers in sclient are binary. See also the lowercase command.

# mkdir <directory na>