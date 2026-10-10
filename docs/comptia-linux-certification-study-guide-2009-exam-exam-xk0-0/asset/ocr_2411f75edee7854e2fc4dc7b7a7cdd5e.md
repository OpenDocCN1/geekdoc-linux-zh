change the permissions of files located within the filesystems. There may be many system administrators on a given system, particularly those located in a large corporation. The number of users who are elevated to this level should be kept to a minimum to ensure the security and integrity of the underlying system. There is a special superuser known as `root`, with a user ID and group ID of 0. This user has full and unrestricted rights to manipulate any file, to traverse to any directory, and to execute any program. For obvious reasons of security, this user’s credentials should be shared by very few people.

The third type of account is that of a system user, which is really not a user at all. This account is an administrative account that is used by the system itself for the running of various administrative tasks. For example, `xfs` owns the X11 font server and all its associated files, and these can be executed only by itself and the root account. System users differ from other users on the system in that they do not have a home directory or password nor can they be accessed via the normal system login prompt.

# System and User Profile and Environment Variables

The following will describe the user profiles that are created for each individual user and the common variables that are modified to suit your personal preference. Each user on the system is able to customize their profile to suit their specific needs and preferences. These preferences are held in environment variables located in resource files throughout the system.

The three different shells in bash are the login shell, the normal shell, and the interactive shell. The login shell reads the .profile file located in the user home directory or /etc directory (~/profile), and interactive shells read `~/ .bashrc`. The environment variables are named objects that contain information that can be used by one or more applications.

As bash is the default shell under Linux, a summary of the bash startup files is shown below:

+   1. `/etc/profile` This is the system-wide startup file and will be executed when a user logs on. The file will be protected, and only the superuser [root] will be able to make changes to the file. As this file may be overwritten with a system upgrade, it is not recommended that changes are made to this directly.

+   2. `/etc/bash.bashrc` This is often linked to /etc/bashrc, and is called *per interactive shell startup*. The file will be protected, and only the superuser [root] will be able to make changes to the file. As this file may be overwritten with a system upgrade, it is not recommended that changes are made to this directly.