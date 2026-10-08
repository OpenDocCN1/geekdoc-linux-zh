# telnet

undefined variable

Remove variable from the list of environment variables. Export variable.

unexport variable

Mark the variable to not be exported unless explicitly requested by the remote side.

? Print help information for the environ command.

logout

Send the telnet logout option to the remote side. This command is similar to a close command. However, nothing happens if the remote side does not support the logout option. If the remote side does support the logout option, this command should close the remote side of the TELNET connection. If the remote side also supports the concept of suspending a user's session for later reattachment, the logout argument indicates that the remote side should terminate the session immediately.

mode type

The remote host is asked for permission to go into the requested mode. If the remote host is capable of entering that mode, enter the requested mode, type is one of the following.

character

Disable the LINEMODE option, or if the remote side does not understand the LINEMODE option, enter "character-at-a-time" mode.

edit (-edit)

Try to enable (disable) the EDIT mode of the LINEMODE option. The LINEMODE option must be enabled.

isig (-isig)

Try to enable (disable) the TRAPSIG mode of the LINEMODE option. The LINEMODE option must be enabled.

line

Enable the LINEMODE option, or if the remote side does not understand the LINEMODE option, try to enter "old-line-by-line" mode.

litecho (-litecho)

Try to enable (disable) the LIT_ECHO mode of the LINEMODE option. The LINEMODE option must be enabled.

softtabs (-softtabs)

Try to enable (disable) the SOFT_TAB mode of the LINEMODE option. The LINEMODE option must be enabled.

? Print help information for the mode command.