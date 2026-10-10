When used with the –D option, this command enables you to update existing user accounts. See the table Account Updating Options for the options you can use in this mode.

See also *userdel*.

**TIP** To determine whether your system creates user’s home directories by default, when you run *useradd*, examine */etc/login.defs*. If you see the line *CREATE_HOME* yes, *useradd* will automatically create a new home directory for each new user and will copy all the files found in */etc/skel* to this directory.

# ACCOUNT CREATION OPTIONS

| Use This Option | To Do This |
|---|---|
| –c comment | Insert the specified comment in the user’s profile. |
| –d directory | Create the user’s home directory with the specified directory name instead of the default /home/username. |
| –e date | Expire the account on the specified date. The date is specified in the format YYYYMMDD. |
| –f days | Disable the account after the password has been inactive for the specified number of days. |
| –G group | Add the user to the specified initial login group. |
| –G group | Add the user to the specified supplementary group. To add the user to more than one group, type group names in a comma-separated list. |
| –m | If this option is not configured by default in /etc/login.defs, create the user’s home directory and copy to this directory the files found in /etc/skel. |
| –M | Skip creating the home directory, even if automatic home creation is enabled by default in /etc/login.defs. |
| –n | Skip creating a group with the same name as the new user. |