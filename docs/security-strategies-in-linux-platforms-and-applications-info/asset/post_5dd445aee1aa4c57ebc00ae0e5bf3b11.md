
# 88 PART 2 | Layered Security and Linux

| TABLE 4-4 Data in /etc/shadow, by column |
| COLUMN | DESCRIPTION |
| --- | --- |
| Groupname | Most Linux systems are configured with users as members of their own group. Other groups may be administrative and more. |
| Password | Normally set to ! if there's no password. |
| Group administrator | A user who is authorized to add users to the group. |
| Group members | A comma-delineated list of users who are members of the group |

| TABLE 4-5 /etc/login.defs security-related directives for new users and groups |
| DIRECTIVE | DESCRIPTION |
| --- | --- |
| FAILLOG_ENAB | Failed login attempts are collected in the binary /var/log/faillog file, unless pam_tally is configured in PAM (described later in this chapter) |
| LOG_OK_LOGINS | Successful logins are collected in a log file defined by /etc/syslog.conf |
| SYSLOG_SU_ENAB | Uses of the su command are logged |
| SYSLOG_SG_ENAB | Uses of the sg command are logged |
| FTMP_FILE | Login failures collected in an associated file |
| PASS_MAX_DAYS | Maximum number of days a password can be used |
| PASS_MIN_DAYS | Minimum number of days a password must be retained |
| PASS_MIN_LENGTH | Minimum password length |
| LOGIN_TIMEOUT | Maximum time for a console login |

# CHAPTER 4 | User Privileges and Permissions

# Defaults for the Shadow Password Suite

When you create new users and groups, the settings are based on defaults configured in the /etc/login.defs file. If you are interested in more rigorous security, you may consider setting or changing the configuration directives shown in Table 4-5.

A number of directives associated with PAM, described later in this chapter, superseded a number of directives traditionally used in /etc/login.defs. For newly created users, the contents of the /etc/skel/ directory are copied to user's home directory with appropriate permissions.

# Privileged and Unprivileged User and Group ID Numbers

Every user and group has a user ID (UID) and group ID (GID) number. With the release of Linux kernel 2.6 in 2003, the number of available UIDs and GIDs was raised from a 16-bit number to a 32-bit number. In other words, the highest legal UID and GID numbers are somewhere around 4 billion. That should be more UID and GID numbers than needed in any modern enterprise. UIDs and GIDs are further limited, however. The /etc/login.defs file defines standards for numbers with the UID_MIN and GID_MIN directives. Depending on the distribution, the minimum UID and GID number for a regular user or group may be 100, 500, 1000, or some other relatively low number. UIDs and GIDs below minimum are reserved for administrative, service, and other privileged accounts.

You'll also find maximum UIDs and GIDs defined in /etc/login.defs. These are arbitrary numbers. UIDs and GIDs above that are often used by other authentication systems as NIS, LDAP, and Microsoft authentication through Samba.

Special high UIDs are associated with fewer privileges than a regular user. Two examples are the users nobody and nobody. They may be assigned the second-to-last possible 16- or 32-bit UID. For example, the account on an Ubuntu system may be assigned a UID number of 65534, the second-to-last possible 16-bit UID. In contrast, the nobody account on a Red Hat system may have a UID number of 429467294, the second-to-last possible 32-bit UID. These accounts have matching GID numbers.

While accounts with such UID and GID numbers are supposed to have fewer privileges than regular users, that's documented only in the information in the user-authentication database.

![](img/c0608a8c8a0777903dfec4ff61fdffa1_114_0.png)

# PART 2 | Layered Security and Linux

| TABLE 4-6 | Standard user- and group management commands |
| COMMAND | DESCRIPTION |
| useradd | Adds users |
| usermod | Modifies users |
| userdel | Deletes users |
| groupadd | Creates a new group |
| groupmod | Modifies a group |
| groupdel | Deletes a group |
| groups | Lists group membership |
| chage | Revises aging for user |

# Shadow Password Commands

A variety of commands are available to create, modify, or delete users. Generally, those shown in Table 4-6 relate to the password suite.

# Variety of Choices

The groups described in this section apply only to Ubuntu. It's certainly possible to configure other Linux distributions with such group privileges, however. To do so, you'll need to do the following:

-   If the specified groups don't already exist on the target distribution, /etc/group and /etc/shadow configuration files, you may need to create them.
-   On an Ubuntu system, identify the groups owned by the noted group. One method is with the find command. For example, the following command identifies those files owned by dip group.
-   # find -group dip
