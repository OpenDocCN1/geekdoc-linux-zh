This gives the status of the account. The value of 0 says disable the account when the password expires. A value of -1 says not to disable it. The default is the value of INACTIVE in Figure 94.

-g initial_group

The initial group that a user logs in with. This can be a name or number of a currently existing group. This is specified in the /etc/password file as the GID or Group ID value. The default group is given by the value of GROUP in Figure 94.

-G group{...}

This is a list of any additional groups the user may belong to. Each group is separated by a comma.

-m [-k skeleton_dir]

The -m option says to create the user's home directory if it does not exist. The skeleton_dir is the location of files that are copied to a new user's directory. The default location, if you do not use the -m option, is the /etc/skeleton directory. The default is the value of SKEL in Figure 94.

-s

This is the shell that the user will log in with. The default is the value of SHELL in Figure 94.

-u uid [-o]

This is the numeric UID or ID number that is used by Linux to distinguish one user from the other. All UIDs must be unique unless the -o option is used. The -o option is often used for creating UIDs that have the same access rights, but different logins and passwords. The system looks only at the UID and GID values for determining access rights.

-r

This is used to create a system account whose UID is lower than a certain number defined in /etc/login.defs. You will also need to specify the -m option if you want to create the home directory. Otherwise, it will not be created. System accounts generally have UID values between 0 and 99.

login

This is the login name that the user will log in with. This will need to be unique on the system.