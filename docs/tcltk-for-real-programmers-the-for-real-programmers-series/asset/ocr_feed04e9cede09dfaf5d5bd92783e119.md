# 3.4 Input/Output in Tcl

# Read 5 characters from stdin
% read stdin 5 # A user types Hello, World
Hello

# 3.4.3 Opening Channels

A channel can be created by an open command or by a socket command.
The open command can be used to open a channel to a file, a device, or
pipe to another program. The socket command can be used to open a cli-
nent socket to a server or to open a server socket that will listen for clients.

The open command is used to create a channel to a file, device, or to
another program.

Syntax: open fileName ?access? ?permissions?

+   * open Open a file, device, or pipe as a channel and return a han-
dle to be used to access this channel.

+   * fileName The name of the file or device to open.
If the first character of the name is a pipe (|), then the file-
name argument is a request to open a pipe connection to the com-
command. The first word in the filename will be the com-\mand name, and subsequent words will be arguments to
the command.

+   * ?access? How this file will be accessed by the channel. Access may
be one of:

+   * r Open file for read-only access.

+   * r+ Open file for read and write access. File
must already exist.

+   * w Open file for write-only access. Truncate
file if it exists.

+   * w+ Open file for read and write access. Trun-\cate the file if it exists, or create it if it
does’t exist.