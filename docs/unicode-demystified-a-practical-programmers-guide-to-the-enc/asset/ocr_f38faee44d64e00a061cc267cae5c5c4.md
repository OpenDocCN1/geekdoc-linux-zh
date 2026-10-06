`cd directory` Changes to a working directory named `directory` on the remote system.

`close` Closes the connection to the remote system without exiting from ftp.

`dir [directory] [file]` Displays a listing of `directory` from the remote system. When you do not specify `directory`, the working directory is displayed. When you specify `file`, the listing is saved on the local system in that `file`; if not, it goes to standard output.

`get remote-file [local-file]` Copies `remote-file` to the local system under the name `local-file`. Without `local-file`, ftp uses `remote-file` as the filename on the local system. The `remote-file` and `local-file` names can be

`glob` Toggles filename extension for `mget` and `mput` commands and tells you what the current state is (Globbing on or Globbing off).

`help` Displays a list of commands recognized by the ftp utility on the local system.

`lcd [directory]` Changes the working directory on the local machine to `local`. Without an argument this command changes the working directory on the local machine (just as `cd` does without argument).

`ls [directory]` Similar to `dir` but produces a more concise listing on remote computers.

`mget remote-file-list multiple` Unlike the get command, the `mget` command allows you to retrieve multiple files from the remote system. You can name the remote files literally or use wildcards (see glob). Also see prompt.

`mput local-file-list multiple` The `mput` command allows you to pull multiple files from the local system onto the remote system. You can name the files literally or use wildcards (see glob). Also see prompt.

`open` Interactively specifies the name of the remote system. If you did not specify a remote system on the command line or if the attempt to connect to the system failed.

`prompt` When using `mget` or `mput` to receive or send multiple files, ftp asks for verification (by default) after each file. This command toggles that behavior and tells you what the current state is (Interactive mode off or Interactive mode on).

`pwd` Causes ftp to display the pathname of the working directory on the remote computer. Use `!pwd` to display the name of the local working directory.

`put local-file [remote-file]` Copies `local-file` to the remote system under the name `remote-file`. Without `remote-file`, ftp uses `local-file` as the filename on the remote system. The `remote-file` and `local-file` names can be pat.

`quit` Quits the ftp session. Same as bye.

`user-name` If the ftp utility did not log you in automatically, you can specify your account name interactively with this command.