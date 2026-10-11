
You should never directly edit the `/etc/shadow` or `/etc/gshadow` files. When you need to change a user's or group's password, use a utility such as `useradd`, `passwd`, `usermod`, or `gpasswd` to make changes to it.

To begin using shadow passwords, use the `pwconv` command, which takes no arguments. When you run this command, it creates a `/etc/shadow` file from your `/etc/passwd` file. You always can convert back by using the `pwunconv` command. Using the `pwunconv` command will update your `/etc/passwd` file and then delete the `/etc/shadow` file.

To use shadow passwords for groups, use the `grpconv` command. This will create a `/etc/gshadow` file and change all the passwords in the `/etc/group` file to x. To revert to saving group passwords in the `/etc/group` file, run the command `grpunconv`.

If you must edit the `/etc/passwd` and `/etc/group` files by hand, you can update your shadow passwords by rerunning the appropriate commands—`pwconv` for `/etc/passwd` and `grpconv` for `/etc/group`. A better way is to first use `pwunconv` and `grpunconv` to stop using shadow passwords, make your changes, and then convert back to using shadow passwords.

## Key Concept

> Shadow passwords increase the security of your system. Use `pwconv` to implement shadow passwords for your users and `grpconv` to use shadow passwords for your groups.

## User Startup Files

The look and function of your shell results from the use of environment variables. These parameters are saved in various configuration files located either in `/etc` or `/home/username/`. The default environment variables for bash when started as an interactive login shell are located in the `/etc/profile` file. The following is an example of a profile file:

```bash
# /etc/profile
# System wide environment and startup programs
# Functions and aliases go in /etc/bashrc

PATH="$PATH:/usr/X11R6/bin"
PATH="$PATH:/usr/local/bin/blender"
PS1='\u@\h \W]\$'
BLENDERDIR=/usr/local/bin/blender
export BLENDERDIR
```

```bash
JAZZ=/usr/local/jazz
export JAZZ

ulimit -c 1000000
if [ `id -gn` = `id -un` -a `id -u` -gt 14 ]; then
    umask 002
else
    umask 022
fi

USER=`id -un`
MAIL="/var/spool/mail/$USER"

HOSTNAME=`/bin/hostname`
HISTSIZE=1000
HISTFILESIZE=1000
export PATH PS1 HISTNAME HISTSIZE HISTFILESIZE USER LOGNAME MAIL

for i in /etc/profile.d/*.sh ; do
    if [ -x $i ]; then
        . $i
    fi
done
```

Notice how the environment variables (such as the system *umask*), path, hostname, and history size are identified. See Chapter 5 for additional information on environment variables.

To make systemwide changes in your user’s environment, make the changes in this file. For example, you might want to add a directory to the path or change the default system prompt. To prevent bash from executing the commands in the profile file, use the `--no-profile` option.

If the user wants some of the default variables to be different, startup files can be placed in the user’s home directory. Copy the `/etc/profile` file to `*.profile` in the user’s home directory and change the ownership of the new file to the user. Now, the user can change any startup parameters, such as her prompt, and they will apply only to that user.

When you create a new user, the defaults located in the /etc/profile file are read and executed to create the user’s environment. Next, the shell looks for the files .bash_profile, .bash_login, and .profile in the user’s home directory.

If one or more of these files is found, they are read and executed in the order listed. If the same environment variable is set in all these files, the variable is set to the last value read. So, if you want to change your path to something different from the system path as defined in the /etc/profile file, you can make that change in the .profile file in your home directory. Because this file is the last one read, whatever value it sets will be the value applied to that user’s environment. Chapter 5 discusses environmental variables in more depth. When exiting an interactive login shell, bash will read and execute the commands in /home/<username>/.bash_logout if it exists.

When a bash shell starts an interactive shell that is not a login shell, such as when you type bash <enter> at a command prompt, it reads and executes the commands in the file /etc/bashrc. This file also can be called from within the profile file. An example of a bashrc file is:

```bash
# /etc/bashrc

# System wide functions and aliases
# Environment stuff goes in /etc/profile

# For some unknown reason bash refuses to inherit
# PS1 in some circumstances that I can't figure out.
# Putting PS1 here ensures that it gets loaded every time.
PS1="${USER}|${PWD}> "
alias lsa="ls -aF --color | more"
alias lsl="ls -l --color | more"
alias rm="rm -i"
alias cp="cp -i"
alias mv="mv -i"
alias cl="clear"
alias dira="dir --color | more"
alias dl="dir -aF --color | more"
```

When starting bash as an interactive non-login shell, you can inhibit this behavior by using the `--norc` option. You also can specify another file to read instead of bashrc by using the `--rcfile <filename>` option, which will cause bash to execute the commands from the specified file instead.

When bash is called as a non-interactive shell, such as when running a shell script, it looks for the environment variable `BASH_ENV`. This variable can contain the name of a file other than the bashrc file to execute. The entire path as well as the file's name is required when setting this variable.

Bash can be invoked using the name sh instead of bash. When invoking bash in this manner, bash examines the value of the ENV variable to identify what file to execute. No other startup files are processed when calling bash in this manner.

An easy way to make sure your new users receive copies of these files in their home directories is to create the appropriate files and save them to /etc/skel. Whenever you create a new user with the useradd command, these files are copied to the new user's directory and the permissions are appropriately set.

![](img/8dd1e68596303df43cb8ccf3197e8e53_194_0.png)

> If you choose to create startup files and manually copy them to the user's home directory, be sure you make the user the owner of these files and set the group ownership appropriately. Failure to do this can result in the user being unable to log on or environment variables being inappropriately set.

## Summary

Managing users and groups is a significant part of any administrator's job. All user accounts are contained in the /etc/passwd file. Each user is defined in a single line and the fields are:

- Username
- Password
- User ID
- Group ID
- Comment
- Home directory
- Login command

Each of these fields, which can be blank, is required.

You can create users by editing the /etc/passwd file or using the useradd command. Other commands used to manage users are usermod and userdel.

The `su` command is used when you want to impersonate another user. If you are root when you issue the `su` command to impersonate a user, you do not need to provide a password. If you are a user, however, you will need to supply the correct password for the command to complete successfully.

Groups are defined in the `/etc/group` file. Each group is listed in a separate line. Groups can be managed by editing the `/etc/group` file or using the `groupadd`, `groupmod`, `groupdel`, or `gpasswd` commands.

Several different configuration files are read by the system in different circumstances. The default files for an interactive, login shell are `/etc/bash_profile`, `/etc/bash_login`, and `/etc/profile`. These files can be copied to the user’s home directory to make changes that will apply to that user only.

Other configuration files are `.bash_logout` and `/etc/bashrc`. Two environment variables that affect the behavior of your shell are `BASH_ENV` and `ENV`.

- Group name
- Password
- Group ID
- Members

Additional security can be implemented by using shadow passwords for users and groups.
