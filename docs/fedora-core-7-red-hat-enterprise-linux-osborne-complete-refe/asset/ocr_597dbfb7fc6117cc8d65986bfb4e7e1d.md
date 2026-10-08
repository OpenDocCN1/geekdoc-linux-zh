```
if [ -z "$EUID" -a -x /usr/bin/id ]; then
            EUID='id -u'
            UID='id -ru'
fi

# Path manipulation
if [ "$EUID" = "0" ]; then
            pathmunge /sbin
            pathmunge /usr/sbin
            pathmunge /usr/local/sbin
fi

# No core files by default
ulimit -S -c 0 > /dev/null 2>&1

if [ -x /usr/bin/id ]; then
            USER="'id -un'"
            LOGNAME=$USER
            MAIL="/var/spool/mail/$USER"
fi

HOSTNAME='/bin/hostname'
HISTSIZE=1000

if [ -z "$INPUTRC" -a ! -f "$HOME/.inputrc" ]; then
            INPUTRC=/etc/inputrc
fi

export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE INPUTRC

for i in /etc/profile.d/*.sh ; do
        if [ -r "$i" ]; then
                . $i
        fi
done
unset i
unset pathmunge
```

# Configuring the BASH Shell: .bashrc

The **.bashrc** file is a configuration file executed each time you enter the BASH shell or generate any subshells. If the BASH shell is your login shell, **.bashrc** is executed along with your **.bash_login** file when you log in. If you enter the BASH shell from another shell, the **.bashrc** file is automatically executed, and the variable and alias definitions it contains will be defined. If you enter a different type of shell, the configuration file for that shell will be executed instead. For example, if you were to enter the TCSH shell with the `tcshtc` command, the **.tcshrc** configuration file would be executed instead of **.bashrc**.

# The User .bashrc BASH Script

The **.bashrc** shell configuration file is actually executed each time you generate a BASH shell, such as when you run a shell script. In other words, each time a subshell is created,