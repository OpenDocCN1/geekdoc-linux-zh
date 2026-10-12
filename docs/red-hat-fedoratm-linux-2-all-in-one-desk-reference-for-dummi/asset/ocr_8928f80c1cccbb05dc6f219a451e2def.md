You see a list of files such as the following:

```
/usr/bin/chage
/usr/bin/gpasswd
/usr/bin/chfn
/usr/bin/chsh
/usr/bin/newgrp
/usr/bin/passwd
/usr/bin/at
/usr/bin/rcp
/usr/bin/rlogin
/usr/bin/rsh
/usr/bin/sudo
/usr/bin/crontab
... lines deleted ...
```

Many of the programs have the setuid permission because they need it, but check the complete list and make sure that there are no strange setuid programs (for example, setuid programs in a user’s home directory).

If you want to see how these permissions are listed by the `ls` command, type `ls -l /usr/bin/passwd` and you see the permission settings:

```
-r-s--x--x  1 root     root        16128 Jun  5 23:03 /usr/bin/passwd
```

The s in the owner’s permission setting (r-s) tells you that the setuid permission is set.

# Using exec-shield

Buffer overflow is (if you’ll pardon the expression) the root cause of many Linux security holes. When buffer overflow occurs, a cracker can overwrite data-storage areas of memory with instructions designed to execute nasty commands. But what if the Linux kernel refuses to execute instructions from any data area? Poof! — no more buffer overflows! That’s exactly what the latest Linux kernel does: It protects against the common buffer overflow type of vulnerabilities by making many parts of a program’s memory (including the stack where temporary variables are stored) not executable. This feature of the Linux kernel is called exec-shield.

The best part about exec-shield is that you don’t have to fix the applications that have the buffer-overflow problem. All you have to do is turn on the feature. To make the process even easier, Fedora Core enables exec-shield by default.