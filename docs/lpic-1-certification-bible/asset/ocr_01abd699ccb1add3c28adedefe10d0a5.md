| **Access Control** | **Function** |
| --- | --- |
| limit <class> <n> <times> | Limits the <class> to <n> number of users connected |
|  | during <times>. If the limit is reached the |
| <message_file> | <message_file> is displayed. |
| noretrieve | Blocks the retrieval of certain files. Paths can be set to |
| [absolute\|relative] | either absolute or relative, and restricted by class. This is |
| [class=<classname>] ... | useful for blocking the downloading of the /etc/ |
| [-] <file name> ... | passwd file. |
| <filename> ... |  |
| allow-retrieve | Allows files to be retrieved that would normally be |
| [absolute\|relative] | blocked by the noretrieve entry. |
| [class=<classname>]... |  |
| [-] <filename> ... |  |
| loginfails <number> | After <number> of attempts to enter the correct |
|  | password, the FTP connection is disconnected. |
| private <yes\|no> | Allows the user to change to a different group using the |
|  | SITE GROUP and SITE GPASS commands. The group |
|  | must be specified in the /etc/ftpgroups file. |
| **Logging** | **Function** |
| log commands <typelist> | Logs commands for user types specified in <typelist>. |
|  | These are real, anonymous, and guest. |
| log transfers <typelist> | Logs transfers by <typelist>. <directions> are |
| <directions> | either inbound or outbound. |
| log security <typelist> | Logs security violations for the user type specified in |
|  | <typelist>. The violations are things such as trying to |
|  | download files protected by noretrieve. |
| **Miscellaneous Capabilities** | **Functions** |
| alias <string> <dir> | Creates an alias that refers to a directory. Used only by |
|  | the cd command. |
| cdpath <dir> | Defines a search path for directories. If a user should |
|  | enter cd foo, the current directory and those listed with |
|  | cdpath will be checked. |
| compress <yes\|no> | Enables the compress function so files can be shrunk |
| [<classglob> ...] | before downloading. |
| tar <yes\|no> <classglob> | Enables the tar function. |
| [[<classglob> ...] |  |