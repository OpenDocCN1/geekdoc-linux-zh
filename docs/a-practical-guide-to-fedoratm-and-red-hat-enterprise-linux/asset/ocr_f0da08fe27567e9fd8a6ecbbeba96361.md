# **Files**

`chmod` *mode* *remote-file*

Changes the access permissions of *remote-file* on the server to *mode*. See `chmod` on page 193 for more information on how to specify the *mode*.

`delete` *remote-file*

Removes *remote-file* from the server.

`mdelete` *remote-file-list*

(multiple *delete*) Deletes the files specified by *remote-file-list* from the server.

# **Display Information**

`?` (question mark) Same as `help`.

`dir` [*remote-directory* \| *file*]

Displays a listing of *remote-directory* from the server. When you do not specify *remote-directory*, displays the working directory. When you specify *file*, the listing is saved on the local system in a file named *file*.

`help` [*command*]

Displays information about *command*. Without *command*, displays a list of local `ftp` commands. Also `?`.

`ls` [*remote-directory* \| *file*]

Similar to `dir` but produces a more concise listing from some servers. When you specify *file*, the listing is saved on the local system in a file named *file*.

`pwd`

Displays the pathname of the working directory on the server. Use `!pwd` to display the pathname of the local working directory.

`rstatus`

Displays `ftp` connection and status information for the local system (client).

`status`

Displays `ftp` connection and status information for the remote system (server).

`verbose`

Toggles and displays verbose mode, which displays responses from the server and reports how quickly files are transferred. The effect of this command is the same as specifying the `-v` option on the command line.

# # Setting up an FTP server (vsftpd)

This section explains how to set up an FTP server implemented by the `vsftpd` daemon as supplied by Fedora/RHEL.

# ## Prerequisites

Install the following package:

+   * `vsftpd`

Run `systemctl` to cause the `vsftpd` service (`vsftpd` daemon) to start each time the system enters multiuser mode and then start the `vsftpd` service. Use the `systemctl` status command to make sure the service is running.