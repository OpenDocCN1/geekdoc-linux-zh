```
```
KDEDIRS=/usr
LANG=en_US.UTF-8
LESSOPEN='||/usr/bin/lesspipe.sh %s'
LINES=59
LOGNAME=root
MACHTYPE=x86_64-redhat-linux-gnu
MAIL=/var/spool/mail/root
MAILCHECK=60
OPTERR=1
OPTIND=1
OSTYPE=linux-gnu
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin
PIPESTATUS=( [0]="0" )
PPID=1291
PROMPT_COMMAND='printf "\033[0;$s@%s;$s\007" "$ {USER}" "$ {HOSTNAME%.*, }" "$ {PWD/$HOME/~/} $'
PS1='\u@\h \W $'
PS2='> $'
PS4='$ $'
PWD=/root
QT_GRAPHICSSYSTEM_CHECKED=1
SELINUX_LEVEL_REQUESTED=
SELINUX_ROLE_REQUESTED=
SELINUX_USE_CURRENT_RANGE=
SHELL=/bin/bash
SHELLOPTS=braceexpand:emacs:hashall:histscript:interactive-comments:monitor
SHLVL=1
SSH_CLIENT='192.168.1.100 43480 22'
SSH_CONNECTION='192.168.1.100 43480 192.168.1.105 22'
SSH_TTY=/dev/pts/0
TERM=xterm
TMP=/tmp/.colorlsn3e
UID=0
USER=root
XDG_RUNTIME_DIR=/run/user/0
XDG_SESSION_ID=2
:
```
```

![](bbox=[0.93, 0.35, 1.0, 0.43])

Some environment variables shown in the preceding output are used by programs that require information about the system; the OSTYPE (Operating System TYPE) and SHELL (Pathname to shell) variables are examples from the preceding output. Other variables are used to set the user's working environment; the most common of these include the following:

+   - $PS1$—The default shell prompt
+   - $HOME$—The absolute pathname to the user's home directory
+   - $PWD$—The present working directory in the directory tree
+   - $PATH$—A list of directories to search for executable programs