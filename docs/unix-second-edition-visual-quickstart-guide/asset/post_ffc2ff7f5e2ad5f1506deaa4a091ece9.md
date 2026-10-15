
# Looking at Your bash Configuration Files

Your first step in modifying or adding bash environment variables in your configuration files is to look at the configuration files, which show you the variables that have been defined.

As Code Listing 8.10 shows, you do this using more or the editor of your choice.

Remember that configuration files run in a specific order:

- Systemwide configuration files (such as /etc/profile) run first upon log in.
- Configuration files specific to your Unix account (such as ~/.bash_profile or ~/.profile) run next if they're available.

## To look at your bash configuration files:

- 1. more ~/.bash* ~/.profile /etc/bash* /etc/profile

At the shell prompt, type more followed by each of the possible system configuration filenames to view your configuration files. If you don't have all of the files mentioned here, don't worry. Just make note of the ones you do have. Code Listing 8.10 shows an example of what you might see. Notice that some of the lines will reference other files, like the ENV=$HOME/.bashrc line that references the .bashrc file, containing other configuration settings.

```
[ejr@hobbes ejr]$ more ~/.bash* ~/.profile /etc/bash* /etc/profile
...
/home/ejr/.bash_profile
...
# .bash_profile
# Get the aliases and functions
```

Code Listing 8.10 Your configuration files set up your environment variables and other features of your Unix experience.

```
if [ -f ~/.bashrc ]; then
  . ~/.bashrc
fi
# User-specific environment and startup programs
PATH=$PATH:$HOME/bin
ENV=$HOME/.bashrc
USERNAME=""
export USERNAME ENV PATH
/home/ejr/.profile: No such file or directory
................
/etc/bashrc
................
# /etc/bashrc
# System-wide functions and aliases
# Environment stuff goes in /etc/profile
# Putting PS1 here ensures that it gets loaded every time
PS1="[\u@\h \W]\$ "
alias which="type -path"
...........
/etc/profile
................
# /etc/profile
# System-wide environment and startup programs
# Functions and aliases go in /etc/bashrc
PATH=$PATH:/usr/X11R6/bin
PS1="[\u@\h \W]\$ "
ulimit -c 10000000
if [ `id -gn` = `id -un` -a `id -u` -gt 14 ]; then
  umask 002
else
  umask 022
fi
USER=`id -un`
LOGNAME=$USER
MAIL="/var/spool/mail/$USER"
HOSTNAME="/bin/hostname"
HISTSIZE=1000
HISTFILESIZE=1000
export PATH PS1 HISTSIZE HISTFILESIZE USER LOGNAME MAIL
for i in /etc/profile.d/* sh ; do
  if [ -x $i ]; then
    . $i
  fi
done
unset i
[ejr@hobbes ejr]$
```

Code Listing 8.10 continued

2. Write down, for your reference, the system configuration files and the order in which they're run. (Remember, settings in the last file run override all previous ones.) Our system configuration files include

- /etc/profile (automatically called by the system if it exists)
- ~/.bash_profile (automatically called by the system if it exists)
- ~/.bashrc (called by ~/.bash_profile)
- /etc/bashrc (called by ~/.bashrc)

Keep in mind that the files you have may differ from the files that we have.

## Tips

- The bash shell sometimes daisychains configuration files together, referencing one from the previous one. Be careful to preserve the references and sequence as you edit your configuration files, or you might end up with unexpected results.
- All lines that start with # are comments, which contain notes to help you better understand the files. Comments don't actually do anything, but they help you see what each file does.

# Adding to Your bash Path

One of the most useful changes you can make to your environment is adding to the default path, which is determined by the path statement. The path statement tells the shell where to look for commands, scripts, and programs. That is, if you issue a command, the path statement tells the system to look for that command in each of the named directories in a specific order.

Be sure not to remove anything from your path unless you really know what you're doing, but feel free to add as many additional directories as you want to it.

As the following steps show, you change your bash path by first identifying where your path statement is located, then editing the file that contains it (Code Listing 8.11).

## To change your bash path:

- 1. more ~/.bash_profile ~/.bashrc
  To begin, view your configuration files (just the ones you can edit) in the order they're executed.
  Look through your system configuration files for a path statement. As Code Listing 8.9 shows, it'll look something like PATH=/bin:/usr/bin:/usr/local/bin.
  If you have more than one path statement, find the last one executed.
  Remember that different systems will have different configurations, so you might need to do a little digging to find your personal path statement(s).

- 2. cp .bash_profile .bash_profile_backup
  Make a backup of the file containing the path statement so that you can recover if you make mistakes. See Chapter 2 if you need more information on copying files.

```
[ejr@hobbes ejr]$ more ~/.bash_profile
... ~/.bashrc
................
/home/ejr/.bash_profile
................
# .bash_profile

# Get the aliases and functions
if [ -f ~/.bashrc ]; then
  . ~/.bashrc
fi

PATH=/bin:/usr/bin:/usr/local/bin

# User-specific environment and startup programs

PATH=$PATH:/usr/local/games
ENV=$HOME/.bashrc
USERNAME=""

export USERNAME ENV PATH

-More-(Next file: /home/ejr/.bashrc)
```

Code Listing 8.11 Your first step is finding out the location of your path statement(s).
