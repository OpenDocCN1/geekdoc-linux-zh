This returns output similar to the following:

```
```
funky is a function
funky ()
{
  ps;
  ls -color=tty -ld;
  who
}
```
```

To set a function in memory, you use the format discussed previously. The following example does three simple and separate tasks that must be delimited by a semicolon (;) character, particularly including the last one after the who command.

This command declares the function funky:

```
```
funky () { ps ; ls -ld ; who ; }
```
```

Executing this function is simple; you just enter it on the command line:

```
```
funky
```
```

This returns output similar to what's shown here:

| PID | TTY | TIME | CMD |
|:----|:----|:-----|:----|
| 4960 | pts/3 | 00:00:00 | bash |
| 5609 | pts/3 | 00:00:00 | ps |

drwxr-x--- 17 root root 8192 Apr 14 15:01 .
root tty1 Apr 8 17:26
root pts/1 Apr 14 14:41 (192.168.1.100)
root pts/0 Apr 8 17:31 (:0)
root pts/2 Apr 12 14:42 (:0)
root pts/3 Apr 14 14:44 (192.168.1.100)

The components of a function can be anywhere from simple to very complex, with just about anything that a script can contain being valid for a function.

Removing a function is relatively simple: If it has been defined in a file such as the .bashrc, you can unset the function for only the current login session with the following command:

```
```
unset funky
```
```

No output is returned—the function just disappears and returns again upon the next login shell.

To remove a function defined on the command line, the same command string is used. A simple logout and login again also refreshes the original session.