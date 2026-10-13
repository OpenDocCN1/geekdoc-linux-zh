```
PATH=$PATH:$HOME/bin:$HOME:
BASH_ENV=$HOME/.bashrc
USERNAME=""
HISTSIZE=30
NNTP SERVER=nntp.myserver.com
EXINIT='set nu ai'
PS1="\w $"
export USERNAME BASH_ENV PATH HISTSIZE EXINIT PS1
```

# Manually Reexecuting the .bash_profile Script

Although .bash_profile is executed each time you log in, it is not automatically reexecuted after you make changes to it. The .bash_profile file is an initialization file that is executed only whenever you log in. If you want to take advantage of any changes you make to it without having to log out and log in again, you can reexecute .bash_profile with the dot (.) command. The .bash_profile file is a shell script and, like any shell script, can be executed with the . command.

```
$ .bash_profile
```

Alternatively, you can use the source command to execute the .bash_profile initialization file, or any initialization file such as .login used in the TC SH shell, or .bashrc.

```
$ source .bash_profile
```

# System Shell Profile Script

Your Linux system also has its own profile file that it executes whenever any user logs in. This system initialization file is simply called profile and is found in the /etc directory. /etc/profile. This file contains system variable definitions the system needs to provide for each user. A copy of the system's .profile file follows. Red Hat uses a pathmunge function to generate a directory list for the PATH variable. The path generated for the root user will look something like this, including both system and user application directories. Normal user paths will lack the system directories, those with sbin in the path, and include the name of their home directory, along with /usr/kerberos/bin for Kerberos tools.

```
# echo $PATH
/usr/local/sbin:/sbin:/usr/sbin:/bin:/usr/bin:/usr/bin/X11:
/usr/X11R6/bin:/usr/local/bin:/usr/bin:/root/bin:/root/bin
```

HISTFILE is also redefined to include a larger number of history events. An entry has been added here for the NNTP SERVER variable. Normally, a news server address is a value that needs to be set for all users. Such assignments should be made in the system's /etc/profile file by the system administrator, rather than in each individual user's own .bash_profile file. The /etc/profile file also executes any scripts in the directory /etc/profile.d. This design allows for a more modular structure. Rather than make entries by editing the /etc/profile file, you can just add a script to profile.d directory. The scripts for the BASH shell have the extension .sh. For example, the kde.sh script in the profile.d directory checks for a definition of the KDEDIR variable and makes one if none is in effect. /etc/profile

```
# /etc/profile
# System wide environment and startup programs, for login setup
# Functions and aliases go in /etc/bashrc
pathmunge () {
    if ! echo $PATH | /bin/egrep -q "(^|:)$1($|:)" ; then
```