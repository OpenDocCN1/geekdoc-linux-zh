This option is primarily useful to work around bugs in some pieces of software that can't handle very large disks, particularly disks over 1GB in size.

*A max disk size of 0 means no limit.*

**max log size (G)** Default: `max log size = 50001000`

This option (an integer in kilobytes) specifies the max size the log file should grow to. Samba periodically checks the size and if it is exceeded it will rename the file, adding a `.old` extension.

A size of 0 means no limit.

**max mux (G)** Default: `max mux = 50`

This option controls the maximum number of outstanding simultaneous SMB operations that Samba tells the client it will allow. You should never need to set this parameter.

**max open files (G)** Default: `max open files = 10000`

This parameter limits the maximum number of open files that one smbd(8) file serving process may have open for a client at any one time. The default for this parameter is set very high (10,000) as Samba uses only one bit per unopened file.

The limit of the number of open files is usually set by the UNIX per-process file descriptor limit rather than this parameter so you should never need to touch this parameter.

**max print jobs (S)** Default: `max print jobs = 10005000`

Example: `max print jobs = 5000`

This parameter limits the maximum number of jobs allowable in a Samba printer queue at any given moment. If this number is exceeded, smbd(8) will remote "Out of Space" to the client.

**protocol** This parameter is a synonym for *max protocol*.

**max protocol (G)** Default: `max protocol = NT1ALLMANMAN1`

Example: `max protocol = LANMAN1`

The value of the parameter (a string) is the highest protocol level that will be supported by the server.

Possible values are :

+   - CORE: Earliest version. No concept of user names.