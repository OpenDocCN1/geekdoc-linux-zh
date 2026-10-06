# Linux Administration: A Beginner's Guide

wildcard expansion. The UNIX method also means that you must be careful where you use the wildcard characters. The wildcard characters themselves in Bash are identical to those in command.com or cmd.exe in the Windows world.
The asterisk (*) matches against filenames, and the question mark (?) matches single characters. If you need to use these characters as part of another parameter for whatever reason, you can escape them by preceding them with a backslash (\) character. This causes the shell to interpret the asterisk and question mark as regular characters instead wildcards.

![](bbox=[0.103, 0.27, 0.163, 0.303])

> NOTE In Linux, wildcards patterns are not exactly the same as regular expressions, although there are some similarities. Wildcards are used for matching filenames, and regular expressions are used for matching text.
The distinction is important, because regular expressions are substantially more powerful than just wildcards alone. All of the shells that contain Linux support regular expressions. You can read more about them in the shell's manual page (for example, man bash, man c, and man tsch) and you can learn more about wildcards and regular expressions in their respective manual pages (man 7 glob and man 7 regex).

# Environment Variables as Parameters

Under Bash, you can use environment variables as parameters on the command line. (Although the Windows command prompt can do this as well, it's not a common practice and thus is an often-forgotten convention). For example, issuing the parameter $FOO will cause the value of the FOO environment variable to be passed rather than the string "FOO".

# Multiple Commands

Under Bash, multiple commands can be executed on the same line by separating the commands with semicolons (;).
For example, here's how to execute this sequence of commands (cat and ls) on two separate lines:

```
[master@server -$] ls -1
[master@server -$] cat /etc/passwd
```

You could indent the following:

```
[master@server -$] ls -1 ; cat /etc/passwd
```

The shell is also a programming language, you can run commands conditionally only if the first command succeeds. This is achieved by using the double ampersand (&&) symbol. For example, you can use the ls command to list a file that does