enter Jun 8 2028 in the change space. Once the user changes his password, the password expiration field is blanked out again, but only the system administrator can extend an account expiration date.

# The Big Hammer: vipw(8)

While chpass(1) is fine for editing individual accounts, what happens when you must edit many accounts? Suppose your system has hundreds of users and a brand new hard disk for the home partition. Do you really want to run chpass(1) hundreds of times? That's where vipw(8) comes in.

Directly edit /etc/master.passwd with vipw(8). When you finish your edits, vipw(8) checks the password file's syntax to be sure you haven't ruined anything. Then, it saves the new password file and runs pwd_mkdb(8). Although vipw(8) can protect your password file from many basic mistakes, if you're clever, you can still muck things up. You must understand the format of the password file to use vipw(8) properly.

If the information in /etc/master.passwd conflicts with information in other files, /etc/master.passwd wins. For example, the primary group that appears in /etc/master.passwd is correct, even if /etc/group doesn't show the user as a member. This “master.passwd is always correct” logic is deeply ingrained throughout user management.

Each line in /etc/master.passwd is a single account record, containing 10 colon-separated fields. These fields are the following:

# Username

This field is either an account name created by the sysadmin or a username created at install time to provide some system service. FreeBSD includes users for system administration, such as root, daemon, games, and so on. Each of these users owns a part of the base system. FreeBSD also provides accounts for common services, such as the www user reserved for use by web servers. Add-on software might add its own system accounts as well.

# Encrypted Password