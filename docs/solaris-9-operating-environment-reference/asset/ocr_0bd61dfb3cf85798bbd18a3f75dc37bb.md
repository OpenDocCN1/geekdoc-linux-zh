# 1282

# shell_builtins

/usr/bin/sh /usr/bin/jsp

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNwcsu |
| CSI | XPG4 Enabled |

/usr/xpg4/bin/sh

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNwxcu4 |
| CSI | Enabled |

# Also

bc(1), echo(1), getoptcvt(1), intro(1), kill(1), ksh(1), login(1), newgrp(1), ps(1), pwd(1), set(1), shell_builtins(1), stty(1), test(1), umask(1), wait(1), rsh(1), su(1), swap(1), sysdef(1M), dup(2), exec(2), fork(2), getlimit(2), pipe(2), ulimit(2), setlocale(3C), signal(3HEAD), passwd(4), profile(4), attributes(5), environ(5), largefile(5), XPG4(5)

# Diagnostics

If you get the error message cannot fork, many processes, try using the wait(1) command to clean up your background processes. If this doesn't help, the system process table is probably full or you have too many active foreground processes. Your login has a limited number of process IDs, and the system can track a limited number.)

When the shell executes a shell script that tries to execute a nonexistent command interpreter, the shell returns an erroneous diagnostic message that the shell file does not exist.

# Warnings

For security reasons, the use of shell built scripts is strictly discouraged.

# shell_builtins — Shell Command Interpreter Built-in Functions

# Description

The sh(1), csh(1), and ksh(1) shell interpreters have special built-in functions that are interpreted by the shell as commands. Many of these built-in commands are implemented by more than one of the shells, and some are unique to a particular shell. The commands are listed in the following table.

| Command | Bourne Shell | Korn Shell | C Shell |
| --- | --- | --- | --- |
| alias | | X | X |
| bg | X | X | X |
| break | X | X | X |