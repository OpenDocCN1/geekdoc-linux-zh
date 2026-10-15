
# Looking at Your ksh Configuration Files

As Code Listing 8.14 (on the next page) shows, you look at your ksh configuration files using more or the editor of your choice. Keep in mind that configuration files are run in a specific order:

- Systemwide configuration files (such as /etc/profile) run first upon log in.
- Configuration files specific to your Unix account (such as ~/.profile) run next if they're available.

## To look at your ksh configuration files:

- 1. more /etc/profile ~/.profile
Type more followed by the names of traditional Korn shell configuration files. You'll see something similar to Code Listing 8.14. As before, look for any other filenames or ENV statements in the listings, which would indicate other files that play a role in getting your ksh environment configured.

- 2. For your own information, list the system configuration files that your system uses and the order in which they're called. For our system, we have
  - /etc/profile (automatically called by the system)
  - ~/.profile (automatically called by the system)

## Tips

- The .profile file is executed when you start a new log-in shell (by logging in or with su - yourid). The .kshrc file is read each time you start any ksh subshell.

## Fill in Your ksh System Configuration Files

The techie term (that you'll likely see in these files) for executing a configuration file or a script is to source it. That is, when you log in, your .profile sources .kshrc.

```
$ more /etc/profile ~/.profile
:::::::::::::::
/etc/profile
::::::::::::::
#ident "@(#)profile 1.1795/03/28 SMI"  /* Svr4.0 1.3 */
# The profile that all logins get before using their own .profile.
trap '' 2 3
export LOGNAME PATH
if [ "$TERM" = "" ]
then
    if /bin/i386
    then
        TERM=AT386
    else
        TERM=sun
    fi
    export TERM
fi
# Login and -su shells get /etc/profile services.
# -rsh is given its environment in its .profile.
case "$0" in
-sh | ksh | -ksh)
    if [ -f ~/.hushlogin ]
    then
        /usr/sbin/quota
    # Allow the user to break the Message-Of-The-Day only.
    trap "trap '' 2" 2
    /bin/cat -s /etc/motd
    trap '' 2
    /bin/mail -E
    case $? in
    0)
        echo "You have new mail."
        ;;
    2)
        echo "You have mail."
        ;;
    esac
    fi
esac
umask 022
trap 2 3
```

Code Listing 8.14 Look for file and path names or ENV statements in the configuration file listings (for the files you have) to identify all of the files that help set up your environment.

```
/home/users/e/ejray/.profile
------------------------
#
PATH=$PATH:$HOME/bin:.  # set command search path
export PATH
if [ -z "$LOGNAME" ]; then
  LOGNAME=`logname`  # name of user who logged in
  export LOGNAME
fi
MAIL=/usr/spool/mail/$LOGNAME # mailbox location
export MAIL
if [ -z "$PWD" ]; then
  PWD=$HOME  # assumes initial cwd is HOME
  export PWD
fi
if [ -f $HOME/.kshrc -a -r $HOME/.kshrc ]; then
  ENV=$HOME/.kshrc # set ENV if there is an rc file
  export ENV
fi
# If job control is enabled, set the suspend character to ^Z (control-z):
case $- in
*m*) stty susp '^z'
::
esac
set -o ignoreeof  # don't let control-d logout
PS1='$ '
export PS1
export ENV=$HOME/.kshrc
------------------------
/home/users/e/ejray/.kshrc
#
# If there is no VISUAL or EDITOR to deduce the desired edit
# mode from, assume vi(C)-style command line editing.
if [ -z "$VISUAL" -o -z "$EDITOR" ]; then
  set -o vi
fi
/etc/ksh.kshrc: No such file or directory
$
```

# Changing Your ksh Path

The path statement tells the shell where to look for commands, scripts, and programs. For example, if you issue a command, the path statement tells the system to look in the named directories in a specific order.

As the following steps show, you change your ksh path by first identifying where your path statement is located, then editing the file that contains it (Code Listing 8.15).

## To change your ksh path:

- 1. grep PATH ~/.profile ~/.kshrc
To begin, check for path statements in the configuration files located in your home directory. If you wanted, you could also review the /etc/profile file, but you cannot edit that one.

- 2. Look through your system configuration files for a path statement. As Code Listing 8.15 shows, it'll look something like PATH=/usr/bin:/usr/local/bin:/usr/sbin. Remember, if you have more than one path statement, find the last one executed. If you don't have a path statement in your personal configuration files at all, then add one.

- 3. cp ~/.profile ~/.profile.backup
Make a copy of the file containing the path statement so that you can recover if you make mistakes. See Chapter 2 if you need more information on copying files.

- 4. vi ~/.profile
Use the editor of your choice to edit the configuration file with the path statement.

```
$ grep PATH ~/.profile ~/.kshrc
/home/users/e/ejray/.profile:PATH=/usr/bin:/usr/local/bin:/usr/sbin:
/home/users/e/ejray/.profile:export PATH
$
```

Code Listing 8.15 First, find out the location of your path statement(s).
