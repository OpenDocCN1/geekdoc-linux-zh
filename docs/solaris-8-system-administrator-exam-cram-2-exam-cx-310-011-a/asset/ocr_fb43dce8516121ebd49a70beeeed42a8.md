```
```text
Local directory now /export/home/dla
ftp> get file.txt
200 PORT command successful.
150 ASCII data connection for xx  (3448 bytes).
226 ASCII Transfer complete.
local: file.txt remote: file.txt
3529 bytes received in 0.0044 seconds (776.02 Kbytes/s)
ftp> binary
200 Type set to I.
ftp> mget mp*
mget m5eaaNc? n
mget mpfnaOfC? y
200 PORT command successful.
150 ASCII data connection for mpfnaOfC  (16198 bytes).
226 ASCII Transfer complete.
local: mpfnaOfC remote: mpfnaOfC
16726 bytes received in 0.0074 seconds (2219.89 Kbytes/s)
mget mpjAaWMc? y
200 PORT command successful.
150 ASCII data connection for mpjAaWMc  (0 bytes).
226 ASCII Transfer complete.
mget mpqvaOMc? n
ftp> quit
221 Goodbye.
```
```

# The rcp Command

You can also use the rcp(1) command to copy a specified file from the local system to the specified remote system. The destination is specified by using a command-line argument in the form of a *host:path* syntax; *host* is the name of the remote system and *path* (separated by a colon) is the full path to a directory or file. If a different user account is being used on the remote system, it is specified before the *host* separated by a @ symbol. The rcp command uses the remote authentication database.

The following listing shows the dla user account on the local system attempting to copy a file to the home directories of two different user accounts on the remote system named solaris8. Note that the second attempt fails because the remote authentication database on the remote system does not allow the local dla user account to access the remote user account named sarah:

```
```text
$ rcp /tmp/file.txt solaris8:/export/home/dla/file.txt
$ rcp /tmp/file.txt sarah@solaris8:/export/home/sarah/file.txt
permission denied
$
```
```

# Remote Shell Execution

The rsh(1) command can be used to execute a command on a remote system. The remsh command is a symbolic link to the rsh command.