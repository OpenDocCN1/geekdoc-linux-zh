individual. Only a root process can change its own UID and GID. A regular user or any other user on the system that has a UID or GID greater than 500 cannot do the same. Such is the power of root.

![](bbox=[0.13, 0.21, 0.85, 0.23])

> Once the /bin/login process has changed its UID to that of a regular user, the process is entirely one-sided. In other words, a regular user cannot go back to being root.

One of the unique advantages of being root is that you can easily become another user when logged in with superuser privileges. Normally, you cannot become another user without first knowing his or her password. However, root can become user *X* or user *Y* without needing to know that user’s password simply due to the privileges granted to the root account.

There are three separate ways to become root and/or another user. Normally, you assume root status by simply entering `su`. This will give you root authority in the same working directory, but *without* the same paths and environments normally granted to the root account. You retain the same environment variables as those of the original user.

You can also become root with *all* the necessary paths and permissions by entering `su -`. This command allows you access to the same accounts normally granted only to users who log in initially as root. Your working directory will also change to the root user’s home directory. This is useful if you want to access any hidden files owned by root. It also provides easy access to files located in directories such as `/sbin`, which is part of root’s environment by default, but not located in other accounts.

The last method of becoming another user while assuming the same permissions, paths, and default locations as that user is to enter `su - <username>`, replacing the username in brackets with the regular account’s username. You can use this method either as root or as yourself. If you use the latter method, you must know that account’s password. If you are executing this command as root, no password is necessary. While logged in as user *X* or user *Y*, you are, for all practical purposes, *that* user and have rights only to files owned by that individual. It is just as easy to delete a regular user’s file as it is to do so as root.