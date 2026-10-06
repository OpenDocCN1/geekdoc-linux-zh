By convention, the exit status of a command that successfully completes is zero. If a command completes with an error, then a positive integer value is placed in the exit status:

```
$ asdfg
-bash: asdfg: command not found
$ echo $?
127
$
```

The invalid command returns an exit status of 127. There's not much of a standard convention to Linux error exit status codes. However, there are a few guidelines you can use, as shown in Table 8-2.

An exit status value of 126 indicates that the user didn't have the proper permissions set to execute the command:

```
$ ./myprog.c
-bash: ./myprog.c: Permission denied
$ echo $?
126
$
```

Another common error you'll encounter occurs if you supply an invalid parameter to a command:

```
$ date %t
date: invalid date `%t'
$ echo $?
1
$
```

TABLE 8-2
Linux Exit Status Codes
| Code | Description |
| 0 | Successful completion of the command |
| 1 | General unknown error |
| 2 | Misuse of shell command |
| 126 | The command can't execute |
| 127 | Command not found |
| 128 | Invalid exit argument |
| 128+x | Fatal error with Linux signal x |
| 130 | Command terminated with Ctl-C |
| 255 | Exit status out of range |