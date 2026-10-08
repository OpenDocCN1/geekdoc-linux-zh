
made earlier by the system's **.profile** file. All these parameter variables are then exported with the **export** command.

## .bash_profile

```bash
# .bash_profile
# Get the aliases and functions
if [ -f ~/.bashrc ];
then
    . ~/.bashrc
fi
# User-specific environment and startup programs
PATH=$PATH:$HOME/bin:$HOME:
unset USERNAME
HISTSIZE=30
NNTPSERVER=news.myserver.com
EXINIT='set nu ai'
PS1="\\w \$"
export PATH HISTSIZE EXINIT PS1 NNTPSERVER
```

# Manually Reexecuting the .bash_profile Script

Although **.bash_profile** is executed each time you log in, it is not automatically reexecuted after you make changes to it. The **.bash_profile** file is an initialization file that is executed *only* whenever you log in. If you want to take advantage of any changes you make to it without having to log out and log in again, you can reexecute **.bash_profile** with the dot (.) command. The **.bash_profile** file is a shell script and, like any shell script, can be executed with the . command.

```bash
$ . .bash_profile
```

Alternatively, you can use the **source** command to execute the **.bash_profile** initialization file, or any initialization file such as **.login** used in the TCSH shell, or **.bashrc**.

```bash
$ source .bash_profile
```

# System Shell Profile Script

Your Linux system also has its own profile file that it executes whenever any user logs in. This system initialization file is simply called **profile** and is found in the **/etc** directory, **/etc/profile**. This file contains parameter variable definitions the system needs to provide for each user. A copy of the system's **.profile** file follows. Fedora and Red Hat use a **pathmunge** function to generate a directory list for the **PATH** variable. Normal user paths will lack the system directories (those with **sbin** in the path) but include the name of their home directory, along with **/usr/kerberos/bin** for Kerberos tools. The path generated for the root user (Effective User ID of 0, EUID = 0) will include both system and user application directories, adding **/usr/kerberos/sbin**, **/sbin**, **/usr/sbin**, and **/usr/local/sbin**, as well as the root user local application directory, **/root/bin**.

```bash
# echo $PATH
/usr/kerberos/bin:/usr/local/bin:/usr/sbin:/bin:/usr/X11R6/bin:/home/richard/bin
```

A special work-around is included for the Korn Shell to set the User and Effective User IDs (**EUID** and **UID**).

The **USER**, **MAIL**, and **LOGNAME** variables are then set, provided that `/usr/bin/id`, which provides the User ID, is executable. The `id` command with the `-un` option provides the user ID’s text name only, like **chris** or **richard**.

**HISTSIZE** is also redefined to include a larger number of history events. An entry has been added here for the **NTPSERVER** variable. Normally, a news server address is a value that needs to be set for all users. Such assignments should be made in the system’s `/etc/profile` file by the system administrator, rather than in each individual user’s own `.bash_profile` file.

> **NOTE** The `/etc/profile` file also executes any scripts in the directory `/etc/profile.d`. This design allows for a more modular structure. Rather than make entries by editing the `/etc/profile` file, you can just add a script to `profile.d` directory.

The `/etc/profile` file also runs the `/etc/inputrc` file, which configures your command line editor. Here you will find key assignments for different tasks, such as moving to the end of a line or deleting characters. Global options are set as well. Keys are represented in hexadecimal format.

The number of aliases and variable settings needed for different applications would make the `/etc/profile` file much too large to manage. Instead, application- and task-specific aliases and variables are placed in separate configuration files located in the `/etc/profile.d` directory. There are corresponding scripts for both the BASH and C shells. The BASH shell scripts are run by `/etc/profile`. The scripts are named for the kinds of tasks and applications they configure. For example, `colorls.sh` sets the file type color coding when the `ls` command displays files and directories. The `vim.sh` file sets the an alias for the `vi` command, executing `vim` whenever the user enters just `vi`. The `kde.sh` file sets the global environment variable `KDEDIR`, specifying the KDE Desktop applications directory, in this case `/usr`. The `krb5.sh` file adds the pathnames for Kerberos, `/usr/kerberos`, to the `PATH` variable. Files run by the BASH shell end in the extension `.sh`, and those run by the C shell have the extension `.csh`.

```bash
/etc/profile
# /etc/profile

# System-wide environment and startup programs, for login setup
# Functions and aliases go in /etc/bashrc

pathmunge () {
        if ! echo $PATH | /bin/egrep -q "(^|:)$1($|:)" ; then
                if [ "$2" = "after" ] ; then
                          PATH=$PATH:$1
                else
                          PATH=$1:$PATH
                fi
        fi
}

# ksh workaround
if [ -z "$EUID" -a -x /usr/bin/id ]; then
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
            USER=`id -un`
            LOGNAME=$USER
            MAIL="/var/spool/mail/$USER"
fi

HOSTNAME=`/bin/hostname`
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

The **.bashrc** shell configuration file is actually executed each time you generate a BASH shell, such as when you run a shell script. In other words, each time a subshell is created, the **.bashrc** file is executed. This has the effect of exporting any local variables or aliases you have defined in the **.bashrc** shell initialization file. The **.bashrc** file usually contains the definition of aliases and any feature variables used to turn on shell features. Aliases and feature variables are locally defined within the shell. But the **.bashrc** file defines them in every shell. For this reason, the **.bashrc** file usually holds aliases and options you would want defined for each shell. In this example, the standard **.bashrc** installed by Fedora for users would included only the execution of the system **/etc/bashrc** file. As an example of how you can add your own aliases and options, aliases for the **rm**, **cp**, and **mv** commands and the shell **noclobber** and **ignoreeof** options have been added. For the root user, **.bashrc**, the **rm**, **cp**, and **mv** aliases have already been included in the root’s **.bashrc** file.

```bash
# .bashrc
# Source global definitions
if [ -f /etc/bashrc ];
then
. /etc/bashrc
fi
set -o ignoreeof
set -o noclobber
alias rm='rm -i'
alias mv='mv -i'
alias cp='cp -i'
```

You can add any commands or definitions of your own to your **.bashrc** file. If you have made changes to **.bashrc** and you want them to take effect during your current login session, you need to reexecute the file with either the **. .bashrc** or the **source** command.

```bash
$ . .bashrc
```

# The System /etc/bashrc BASH Script and the /etc/profile.d Directory

Linux systems usually contain a system **bashrc** file executed for all users. The file contains certain global aliases and features needed by all users whenever they enter a BASH shell. This is located in the **/etc** directory, **/etc/bashrc**. A user’s own **.bashrc** file, located in the home directory, contains commands to execute this system **.bashrc** file. The **. /etc/bashrc** command in the previous example of **.bashrc** does just that. Currently the **/etc/bashrc** file sets the default shell prompt, one for a terminal window and another for a screen interface. Several other specialized aliases and variables are then set using configuration files located in the **/etc/profile.d** directory. These scripts are executed by **/etc/bashrc** if the shell is not the user login shell.

# The BASH Shell Logout File: .bash_logout

The **.bash_logout** file is also a configuration file, but it is executed when the user logs out. It is designed to perform any operations you want done whenever you log out. Instead of variable definitions, the **.bash_logout** file usually contains shell commands that form a kind of shutdown procedure—actions you always want taken before you log out. One common logout command is to clear the screen and then issue a farewell message.

As with **.bash_profile**, you can add your own shell commands to **.bash_logout**. In fact, the **.bash_logout** file is not automatically set up for you when your account is first created. You need to create it yourself, using the Vi or Emacs editor. You could then add a farewell
