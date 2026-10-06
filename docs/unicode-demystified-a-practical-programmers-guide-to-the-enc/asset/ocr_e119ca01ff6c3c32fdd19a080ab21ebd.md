# System Operation 963

/bin/bash is assumed. You can put /bin/tesh to log in using the TC Shell or
/bin/zsh to log in using the Z Shell. The csh utility (page 1056) changes this value for.
The program specified in the right-hand field of each line in the passwd file is
usually a shell but can be any program. The following line in the passwd file creates
a "user" whose purpose is to execute the utility:

```
who:x:1000:1000:execute who:/usr/bin/who
```

Using as a login name causes the system to log in, execute the util-
and log out. The output of which flashes by in a hurry as the new login
prompt clears the screen immediately after finishes running. This entry in the
passwd file does not provide a shell; there is no way for you to stay logged after
finishing executing.

This technique is useful for providing special accounts that may do only one
t. For instance, sites may use an ftp (page 1180) account in order to enable
anonymous FTP FTP access to their systems. Because no one logs in this account, set
the shell to /bin/false (which returns a false exit status) or to /sbin/nologin (which
d not permit the user to log in). When you put a message in /etc/nologin.txt,
nologin displays message (except it has the same problem as the output of:
It is removed so quickly that you cannot see it.

# Do Not Replace a Login Shell with a Shell Script

Be careful when using special shells in place of login shells in /etc/passwd. Do not use scripts
as replacements for shells. A user may be able to interrupt a shell script, giving him or her full shell
access when you did not intend to do so. When installing a dummy shell, use a compiled program, not
as shell script.

/etc/printcap The printer capability database. This file describes printers and is derived
from 4.3BSD UNIX. Refer to page 1012 and the printcap man page.

/etc/profile Contains a system interactive shell initialization script for environment and
start-up programs. When you log in, the first thing the shell does is to execute the
commands in the same file in this manner, refer to the discussion of . [dot] com-
mand on page 581.) This file allows the system administrator to establish system-
wide environment parameters that individual users can override. Using this file, you
can set shell variables, execute utilities, and take care of other housekeeping tasks.
See also "~/.bash_profile" on page 956.