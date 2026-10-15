
Table 7.4 is a handy summary of commands and configuration files related to managing users. Each of our example systems has a suite of commands for manipulating users, usually at least **useradd**, **usermod**, and **userdel**. Since the commands are all configured similarly, we show **useradd** as representative of all three and supplement its entry with other system-specific commands.

Please note that although each vendor has named its tools **useradd**, etc., the tools themselves are different from system to system.

**Table 7.4  Commands and configuration files for user management**

| System | Cmds | Configuration files | Comments |
|---|---|---|---|
| Ubuntu | **useradd**<br>**adduser** | **/etc/login.defs**<br>**/etc/default/useradd**<br>**/etc/adduser.conf** | Friendlier Perl version |
| SUSE | **useradd** | **/etc/login.defs**<br>**/etc/default/useradd**<br>**/etc/default/passwd**<br>**/usr/sbin/useradd.local**<br>**/usr/sbin/userdel.local**<br>**/usr/sbin/userdel-pre.local**<br>**/usr/sbin/userdel-post.local** | For local customizations<br>For local customizations<br>For local customizations<br>For local customizations |
| Red Hat | **useradd** | **/etc/login.defs**<br>**/etc/default/useradd** | |
| Solaris | **useradd** | **/etc/default/{login,passwd}**<br>**/etc/security/policy.conf** | |
| HP-UX | **useradd**<br>**smh** | **/etc/default/useradd**<br>**/etc/default/security** | GUI tool, also called **sam** |
| AIX | **useradd**<br>**mkuser**<br>**chuser**<br>**rmuser**<br>SMIT | **/etc/security/user**<br>**/etc/security/login.cfg**<br>**/etc/security/mkuser.default** | Called by **useradd**<br>Called by **usermod**<br>Called by **userdel**<br>GUI tool |

a. This file is in **/usr/lib/security** on older AIX systems.

## useradd on Ubuntu

Ubuntu provides two ways to add users: **adduser** and **useradd**. **adduser** is a Perl wrapper for **useradd** that is a bit more helpful (makes home directories, copies in startup files, etc.).

**adduser** is configured in **/etc/adduser.conf**, which includes options such as these:

- Rules for locating home directories: by group, by username, etc.
- Permission settings for new home directories
- UID and GID ranges for system users and general users
- An option to create individual groups for each user
- Disk quotas (Boolean only, unfortunately)
- Regex-based matching of usernames and group names

Other typical **useradd** parameters, such as rules for passwords, are set as parameters to the PAM module that does regular password authentication. (See page 908 for a discussion of PAM, aka Pluggable Authentication Modules.) **adduser** has a **twin addgroup** and cousins **deluser** and **delgroup**.

## useradd on SUSE

![](img/14d78e3cecac4581d37024baf1e94cca_241_0.png)

SUSE’s **useradd** does not create a new user’s home directory or copy in startup files by default. You must request these niceties with the **-m** flag. (The startup files come from **/etc/skel**.) Nor does **useradd** create a mail spool file for new users.

SUSE’s **useradd** also does not create user-specific groups; the default GID in the **passwd** file is set by the variable GROUP in **/etc/default/useradd**. New users are also added to the groups specified by the GROUPS variable. By default, these are the groups video and dialout, which allow access to the system’s frame buffer and the dialup IP software **pppd**.

To make up for these deficiencies, SUSE’s **useradd** calls **/usr/sbin/useradd.local**, a **bash** script to which you can add whatever customizations you wish.

The **/etc/login.defs** file on SUSE controls the following types of issues:

- Whether to allow logins if a user’s home directory does not exist
- Degree of tolerance (delay and lockout) for failed login attempts
- Location of the “message of the day” and **ttype** (terminal type) files
- Restrictions on the use of **chsh** and **chfn**
- Password aging
- Ranges of system and user UIDs and GIDs
- Rules for forming valid user and group names
- Users’ **umasks** (the default is 022)
- Local scripts that piggyback on the **useradd** and **userdel** commands

Both the man page for **login.defs** and the comments in the file itself do a good job of describing the various parameters and their meanings.

## useradd on Red Hat

![](img/14d78e3cecac4581d37024baf1e94cca_241_1.png)

The **useradd** program on Red Hat Enterprise Linux takes its configuration parameters from **/etc/login.defs**, where issues such as password aging controls, encryption algorithms, mail spool files, and UID/GID ranges are addressed. The comments in the file do a good job of explaining the various parameters.
