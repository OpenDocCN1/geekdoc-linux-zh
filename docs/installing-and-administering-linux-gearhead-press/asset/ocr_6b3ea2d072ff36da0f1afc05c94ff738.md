```
USER=~`id -un`
LOGNAME=$USER
MAIL="/var/spool/mail/$USER"

HOSTNAME=`/bin/hostname`
HISTSIZE=1000

if [ -z "$INPUTRC" -a ! -f "$HOME/.inputrc" ]; then
INPUTRC=/etc/inputrc
fi
export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE INPUTRC
for i in /etc/profile.d/*.sh ; do
if [ -x $i ]; then
. $i
fi
done
unset i
```

Selected variables from Example 11.7 are described in Table 11.1. The PATH variable lists the directories through which the shell will look for commands that have been issued to it. Note the format of PATH in Example 12.1, especially $PATH, which tells the shell to include all directories listed in previous initialization scripts. Notice also that the shell was told to add the *usr/X11R6/bin* directory to those directories.

The PS1 variable, as discussed previously, sets the format of the primary shell prompt. In Example 11.7, the shell is told to put the username, the name of the user’s computer, and the user’s default home (file) directory in square brackets. The dollar sign (outside the brackets) is the prompt symbol.

With the ulimit command, the shell is provided with the upper limit on system resources that commands and files can use. Check the ulimit man pages or other sources for further information.

As discussed in Chapter 6, “Linux File Permissions,” umask sets the user’s default permissions as owner, group member, and member of “others” for user-created files and directories. In the example, the user ID is subjected to an if-then-else process to set the umask for a root user to 022 and for an ordinary user to 022.

Next, the shell is told that the format for the user account name will be the user’s name on the system, not the user’s ID number as found in /etc/passwd. In other words, any command or script that calls for the variable USER will be given that name in the format specified here.

The LOGNAME variable tells the shell that the user’s login name will be the same as the user’s name stipulated by the USER variable.