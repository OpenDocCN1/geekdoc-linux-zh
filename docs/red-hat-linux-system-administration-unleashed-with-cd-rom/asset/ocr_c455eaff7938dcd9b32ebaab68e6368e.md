# group

This is the same as in /etc/group.

# password

This is the encrypted group password.

# administrators

This is a comma-separated list of userids. These users can add or remove other users from the group.

# members

This is a comma-separated list of userids. These are the members of the group.

# The /etc/login.defs

This file contains default information for account creation and maintenance. This is where all the defaults for useradd/adduser and groupadd are kept. It also contains some settings for GID and UID ranges to use when creating new users and groups.

# The /etc/skel Directory

This directory contains default configuration files to be used when creating new accounts. If you run useradd with home directory creation enabled, any files you put here will be copied into the home directory of the new account. Things to put here would be shell configuration files, window manager configuration files, or any other files or directories you think a new user should have in his or her home directory.

Now that you have a handle on the primary files that are involved, let's look at how user and group accounts can be administered on your Linux system.

# Adding and Deleting User Accounts

If you are going to have users on your system, manipulating user accounts will soon become second nature to you. It does not have to be a chore. There are plenty of tools available to make life easy for the administrator. To properly understand what is happening when users and groups are added and deleted, we will take a ground-up approach to account manipulation and start with adding a user with no tools at all and work our way up to the GUI-driven tools.