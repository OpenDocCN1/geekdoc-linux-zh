phone numbers, etc. Any string of characters must be put double quotes. For example, -c comment "John Doe, rm. 45, 78965".

-d home_dir

The home directory location of the user. If this is not specified then the default is to append the login name to the end of the default value for HOME shown in Figure 6. For example, the home directory for jdoe will be /home/j unless specified here.

-e expire_date

This is the date on which the user account will be disabled. The date is specified in the format MM/DD/YY where MM is the month, DD is the date and YY is the two-digit format of the year. (Note that though the date is represented in two digits, Linux converts the date to a format that is not Y2K dependent, so there are no Y2K worries here.) The default is the value of EXPIRE in Figure 61.

-f inactive_time

This gives the status of the account. The value of 0 says to disable the account when the password expires. A value of -1 says not to disable it. The default is the value of INACTIVE in Figure 61.

-g initial_group

The initial group a user logs in with. This can be a name or number of a currently existing group. This is specified in the /etc/password file as the GID or Group ID value. The default group is given by the value of GROUP in Figure 61.

-g group[...]

This is a list of any additional existing groups the user may belong to. Each group is separated by a comma.

-m [-k skeleton_dir] |M

The -m option says to create the user's home directory if it does not exist. The skeleton_dir is the location of files that are copied to a new user's directory. The default location, if you do not use the -m option, is /etc/skel directory. The default is the value of SKEL in Figure 61.

-s shell

This is the shell that the user will first log in with. The default is the value of SHELL in Figure 61.

-u uid [-o]