**Table 10.8. Commonly Used ftp Subcommands (continued)**

| Subcommand | Description |
|---|---|
| **get remote local** | Copies the file *remote* from the remote system to the file *local* on the local system. If *local* is not specified, the file is given the same name on the local system. |
| **hash** | Prints a pound (#) character for every 8,912 bytes sent or received. |
| **help subcommand** | Displays a short description of *subcommand*. |
| **lcd path** | Changes the local current directory to *path*. |
| **ls** | Lists the contents of the remote directory. |
| **mget meta** | Copies multiple files from the remote system to the local system. A set of files is specified by *meta*, which is an expression with one or more metacharacters. |
| **mput meta** | Copies multiple files from the local system to the remote system. A set of files is specified by *meta*, which is an expression with one or more metacharacters. |
| **put local remote** | Copies the file *local* from the local system to the file *remote* on the remote system. If *remote* is not specified, the file is given the same name on the remote system. |
| **quit** | Exits the ftp command. |

The following example uses the ftp command to access the remote system solaris8 using the dla user account name. Various subcommands (in italics) are used to transfer files between systems:

```
```text
$ ftp solaris8
Connected to solaris8.
220 solaris8 FTP server (SunOS 5.8) ready.
Name (solaris8:dla): dla
331 Password required for dla.
Password:
230 User dla logged in.
ftp> cd /tmp
250 CWD command successful.
ftp> ls
200 PORT command successful.
150 ASCII data connection for /bin/ls (0 bytes).
ab2.socat.cache
dtdbcache_0
file.txt
mp5eaaNc
mpfnaofNc
mpjAwMc
mpqvoaMc
ps_data
sdtvolcheck388
226 ASCII Transfer complete.
100 bytes received in 0.0032 seconds (30.14 Kbytes/s)
ftp> lcd /export/home/dla
```
```