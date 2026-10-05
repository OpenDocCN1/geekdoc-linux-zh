adduser is configured in /etc/adduser.conf, which includes options such as these:

+   - Rules for locating home directories: by group, username, etc.
- Permission settings for new home directories
- UID and GID ranges for system users and general users
- An option to create individual groups for each user
- Disk quotas (Boolean, unfortunately)
- Regex-based matching of usernames and group names

Other typical adduser parameters, such as rules for passwords, are set parameters to the PAM module that does regular password authentication. (See page 908 for a discussion of PAM, Pluggable Authentication Modules.) adduser has a twin addgroup and cousins deluser delgroup.

# useradd on SUSE

SUSE's adduser does not create a new user's home directory or startup files by default. You must request these niceties with the -m flag. (The startup files come from /etc/skel.) Nor does adduser create a spool file for new users.

SUSE's adduser also does not create user-specific groups; the default GID in the passwd file is set by the variable in /etc/default/useradd. New users are also added to the groups specified by the GROUPS variable. By default, these are video and dialout, which allow access to the system's frame buffer and the dialup IP server pppd.

To make up for these deficiencies, SUSE's useradd calls /usr/sbin/useradd.local, a bash script to which you can add whatever customizations you wish.

The /etc/login.defs file on SUSE controls the following types of issues:

+   - Whether to allow logins if a user's home directory does not exist
- Degree of tolerance (delay and lockout) for failed login attempts
- Location of the "message of the day" and ttytype (terminal) files
- Restrictions on use of csh and chfin
- Password aging
- Ranges of system and user UIDs and GIDs
- Rules for forming valid user and group names
- Users' umask (the default is 022)

Local scripts that piggyback on the useradd and userdel commands

Both the main page for login.defs and the comments in the file itself do a good job of describing the various parameters and their meanings.

# useradd on Red Hat

The useradd program on Red Hat Linux takes its configuration parameters from /etc/login.defs, where issues such as password aging controls, encryption algorithms, mail spool files, and UID/GID ranges are addressed. The comments in the file do a good job of explaining the various parameters.

![](bbox=[0.195, 0.377, 0.245, 0.417])

![](bbox=[0.195, 0.857, 0.245, 0.897])