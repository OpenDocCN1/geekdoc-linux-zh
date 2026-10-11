```
[root@server1 root]# alias dw="date;who"
[root@server1 root]# alias
alias cp='cp -i'
alias dw='date;who'
alias l.='ls -d .* --color=tty'
alias ll='ls -l --color=tty'
alias ls='ls --color=tty'
alias mc='. /usr/share/mc/bin/mc-wrapper.sh'
alias mf='mount -t ext2 /dev/fd0 /mnt/floppy'
alias mv='mv -i'
alias rm='rm -i'
alias vi='vim'
alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'
[root@server1 root]# dw
Sun Jun 5 10:25:45 EDT 2005
  root     pts/0    Jun 1 08:44 (3.0.0.2)
  root     pts/1    Jun 1 11:54 (:0)
[root@server1 root]#
```

> **NOTE**
> It is important to use unique alias names because the shell searches for them before it searches for executable files; if you create an alias called who, that alias would be used instead of the who command on the filesystem.

# ## Environment Files

Recall that variables are stored in memory. When a user exits the BASH shell, all variables stored in memory are destroyed along with the shell itself. To ensure that variables are accessible to a shell at all times, you must place variables in a file that is executed each time a user logs in and starts a BASH shell. These files are called **environment files**. Some common BASH shell environment files and the order in which they are executed are listed next:

+   1. /etc/profile
+   2. ~/.bash_profile
+   3. ~/.bash_login
+   4. ~/.profile

The /etc/profile file is always executed immediately after login for all users on the system and sets most environment variables, such as HOME and PATH. After /etc/profile finishes executing, the home directory of the user is searched for the hidden environment files .bash_profile, .bash_login, and .profile. If these files exist, the first one found is executed; as a result,