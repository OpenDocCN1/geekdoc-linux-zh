# Advanced Bash–Scripting Guide

```
error() {
    local format=$1
    shift
    printf "$(gettext -s "$format") "$@" >&2
    exit $E_CDERROR
}

cd $var || error "Can't cd to %s." "$var"
read -p "$(gettext -s "Enter the value: ")" var
...
```

The TEXTDOMAIN and TEXTDOMAINDIR variables need to be exported to the environment.

This appendix written by Stephane Chazelas.

# # Appendix F. History Commands

The shell provides command-line tools for editing and manipulating a user's command history. This is primarily a convenience, a means of saving keystrokes.

Bash history commands:

+   1. history
2. fc

```
bash$ history
1 mount /mnt/cdrom
2 cd /mnt/cdrom
3 ls
3...
```

Internal variables associated with Bash history commands:

+   1. $HISTCMD
2. $HISTCONTROL
3. $HISTIGNORE
4. $HISTFILE
5. $HISTFILESIZE
6. $HISTSIZE
7. !!
8. !#
9. !N
10. !-N
11. !-STRING
12. !STRING?
13. !?STRING
14. ^STRING^string^

Appendix F. History Commands