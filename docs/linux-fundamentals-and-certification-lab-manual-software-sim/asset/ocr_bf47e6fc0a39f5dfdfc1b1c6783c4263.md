![](bbox=[0.31, 0.08, 0.87, 0.31])

# FIGURE 4–3
ls -l command.

Each user and group has a unique identification number. That for the user is called the userid (UID) and for the group, the groupid (GID). The default value of UIDs is typically greater than 99 and one greater than any other user. UID values between 0 and 99 are typically reserved for system accounts. GIDs are typically 100 or greater and by default greater than any other group. GID values between 0 and 100 are reserved for system accounts.

A UID and GID of 0 are used to identify the root account. Linux grants all access to the root user account regardless of file permissions.

When a file is created, it is assigned to a user and a group owner. It is also assigned separate read, write, and execute permissions for the owner, the group, and everyone else. The user and group that own the file can be changed by the root user.

+   Objective 2.20
Objective 4.2

# Adding a User

Users can be added through the command line or the GUI. Most user and group properties have default values that will be used during account creation.

Before adding a user you should be logged in as root. You can connect quickly as the root user by using the **su** command. The su, substitute user, command changes the effective userid and group id to those of a user identified in the command. The syntax of the su command is su [-**options**] [-] [user]. The default user is root if the user is not identified. The hyphen (-) logs in with a new login shell in the designated user’s home directory as if the user had logged in originally. For example, to log in as the root user type **su - root**.

For a user, all that must be identified is the username and password. To create a user from the command line, use the command **useradd username**.

For example, **useradd jsmith** creates an account called jsmith. The following properties were not explicitly defined. Some have a default value; others have no value unless explicitly created.

+   - -c comment The new user’s password file comment field.
- -d home directory This creates a user’s login directory. The default is to append the user’s name to the home directory.
- -e expire date The date this account will automatically be disabled.
- -f inactive days The number of days after a password expires until the account is permanently disabled. This can have a value of 0 to disable the account as soon as the password has expired, and a -1 to disable this feature.
- -g initial group The group name or number of the initial group for this account. The default group number is 1 or whatever is specified in /etc/default/useradd.
- -G group[,...] A list of supplementary groups that the user is a member of. Each group is separated by a comma.