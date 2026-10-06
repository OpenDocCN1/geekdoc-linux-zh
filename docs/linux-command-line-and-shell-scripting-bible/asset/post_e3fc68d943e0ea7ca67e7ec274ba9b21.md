
# Login shell

When you log in to the Linux system, the bash starts as a login shell. The login shell looks for four different startup files to process commands from. The order in which the bash shell processes the files is:

- /etc/profile
- $HOME/.bash_profile
- $HOME/.bash_login
- $HOME/.profile

The /etc/profile is the main default startup file for the bash shell on the system. Every user on the system executes this startup file when they log in. The other three startup files are specific for each user and can be customized for each user's requirements. Let's take a closer look at these files.

# The /etc/profile file

The /etc/profile file is the main default startup file for the bash shell. Whenever you log in to the Linux system, bash executes the commands in the /etc/profile startup file. Different Linux distributions provide different commands in this file. On my Linux system, it looks like:

```
$ cat /etc/profile
# /etc/profile

# System wide environment and startup programs, for login setup
# Functions and aliases go in /etc/bashrc

pathmerge () {
  if ! echo $PATH | /bin/egrep -q "([^|:])$1(|:)"; then
    if [ "$2" = "after" ]; then
      PATH=$PATH:$1
    else
      PATH=$1:$PATH
    fi
  fi
}

# ksh workload
if [ -z "$EUID" -a x /usr/bin/id ]; then
  EUID=`id -u`
  UID=`id -ru`
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
  USER=$(id -un)
  LOGNAME=$USER
  MAIL=$var/spool/mail/$USER
fi

HOSTNAME=`/bin/hostname`
HISTSIZE=1000

if [ -z "$INPUTRC" -a ! -f "$HOME/.inputrc" ]; then
  INPUTRC=/etc/inputrc
fi

export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE INPUTRC
for i in /etc/profile.d/*.sh; do
  if [ -r "$i" ]; then
    . "$i"
  fi
done

unset i
unset pathmunge
```

Most of the commands and scripts you use in this file are covered in more detail later on in Chapter 8. The important thing to notice now is the environment variables that are set in this startup file. Notice the export line near the bottom of the file:

```
export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE INPUTRC
```

This ensures that environment variables are available to all child processes spawned from the login shell.

There's also another feature that the profile file uses. There's a statement that iterates through any files located in the /etc/profile.d directory. (for statements are discussed in detail in Chapter 10.) This provides a place for the Linux system to place application-specific startup files which will be executed when the shell logs in. On My Linux system, I have the following files in the profile.d directory:

```
$ ls -l /etc/profile.d
total 168
-rw-r--r-- 1 root root 88 2007-03-15 10:08 ccache.sh
-rw-r--r-- 1 root root 87 2007-03-15 10:08 ccache.sh
-rw-r--r-- 1 root root 764 2007-07-26 08:04 colors.sh
-rw-r--r-- 1 root root 713 2007-02-26 08:04 colors.sh
-rw-r--r-- 1 root root 80 2007-01-11 09:00 cvs.sh
-rw-r--r-- 1 root root 78 2007-07-11 09:00 cvs.sh
-rw-r--r-- 1 root root 192 2004-09-09 01:17 glib2.sh
-rw-r--r-- 1 root root 192 2005-12-20 12:58 gnome-ssh-askpass.sh
-rw-r--r-- 1 root root 58 2007-03-20 05:17 gnome-ssh-askpass.sh
-rw-r--r-- 1 root root 70 2007-03-20 05:17 gnome-ssh-askpass.sh
-rw-r--r-- 1 root root 218 2004-09-09 00:00 krb5-devel.sh
-rw-r--r-- 1 root root 229 2006-01-19 13:05 krb5-devel.sh
-rw-r--r-- 1 root root 218 2004-09-09 03:12 krb5-workstation.sh
-rw-r--r-- 1 root root 229 2006-01-19 13:05 krb5-workstation.sh
-rw-rxr-x 1 root root 306 2007-06-25 12:57 lang.sh
-rw-rxr-x 1 root root 322 2007-06-25 12:57 lang.sh
-rw-r--r-- 1 root root 122 2007-02-07 07:55 less.sh
-rw-r--r-- 1 root root 108 2007-02-07 07:55 less.sh
-rw-r--r-- 1 root root 74 2007-06-27 05:11 vim.sh
-rw-r--r-- 1 root root 248 2007-06-27 05:11 vim.sh
-rw-rxr-x 1 root root 170 2007-01-22 05:48 lang.csh
```

You'll notice that these are mostly related to specific applications on the system. Most applications create two startup files, one for the bash shell (using .sh extension) and one for csh (using .csh extension). We'll be talking about the differences between these two later in Chapter 2. The lang.csh and lang.sh files attempt to determine the default language set used on the system, and set the LANG environment appropriately.

# The startup files

The remaining three files are all used for the same function—to provide a user-specific startup file for defining user-specific environment variables. Most Linux distributions use only one of these files:

- $HOME/.bash_profile
- $HOME/.bash_login
- $HOME/.profile

# Using Linux Environment Variables

Notice that all files start with a dot, making them hidden files (they don't appear in a normal ls listing). Since they are in the user's HOME directory, each user can edit the files and add his or her environment variables that are active for every bash shell they start.

My Linux system contains the following .bash_profile file:

```
$ cat .bash_profile
# .bash_profile

# Get aliases and functions
if [ -f ~/.bashrc ]; then
  source ~/.bashrc
fi

# User specific environment and startup programs
export PATH=$HOME/bin
```

The .bash_profile startup file first checks to see if there is another startup file present in the HOME directory called .bashrc (which we will talk about next in the "Interactive Shell" section). If so, the startup file executes the commands in it. Next, the startup file adds a directory to the PATH environment variable, providing a common location to place executable files in your HOME directory.

# Interactive shell

If you start a bash shell without logging into a system (such as if you type bash at a CLI prompt), you start what's called an interactive shell. The interactive shell doesn't act like the login shell, but it provides a CLI prompt for you to enter commands. If bash is started as an interactive shell, it doesn't process the /etc/profile file. Instead, it checks for .bashrc file in the user's HOME directory.

On your Linux distribution, this file looks like this:

```
[rich@testbox ~]$ cat .bashrc
# .bashrc

# Source global definitions
if [ -f /etc/bashrc ]; then
  . /etc/bashrc
fi

# User specific aliases and functions

The .bashrc file does two things. First, it checks for a common bashrc file in the /etc directory. Second, it provides a place for the user to enter personal aliases (discussed later in the Using Command Aliases section) and private script functions (described in Chapter 14). The common /etc/bashrc startup file is run by everyone on the system who starts an interactive session. On your Linux distribution it looks like this:

```
$ cat /etc/bashrc
# /etc/bashrc

# System wide functions and aliases
# Environment setup goes in /etc/profile

# By default, we want this to get set.
# Even for non-interactive, non-login shells.
if [ $UID -gt 99 ] && [ "$(id -gn)" = "user" ]; then
    umask 022
else
    umask 022
fi

# are we an interactive shell?
if [ "$PS1" ]; then
    case $TERM in
        xterm)
            if [ -e /etc/sysconfig/bash-prompt-xterm ]; then
                PROMPT_COMMAND=/etc/sysconfig/bash-prompt-xterm
            else
                PROMPT_COMMAND='echo -ne\n\[033]0;$(USER)@$(HOSTNAME%%.*):$(PWD/#$HOME~)\'; echo -ne '\[007\]'
            fi
            ;;
        screen)
            if [ -e /etc/sysconfig/bash-prompt-screen ]; then
                PROMPT_COMMAND=/etc/sysconfig/bash-prompt-screen
            else
                PROMPT_COMMAND='echo -ne\n\[033]_\$(USER)@$(HOSTNAME%%.*):$(PWD/#$HOME~)\'; echo -ne '\[033]\*'
            fi
            ;;
        *)
            if [ -e /etc/sysconfig/bash-prompt-default ] &&
                PROMPT_COMMAND=/etc/sysconfig/bash-prompt-default
            fi
            ;;
    esac
fi
# Turn on checkwinsize
shopt -s checkwinsize
```
