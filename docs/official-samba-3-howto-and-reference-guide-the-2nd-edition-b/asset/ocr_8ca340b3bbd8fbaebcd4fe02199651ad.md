**NOTE**

PAM allows stacking of authentication mechanisms. It is also possible to pass information obtained within one PAM module through to the next module in the PAM stack. Please refer to the documentation for your particular system implementation for details regarding the specific capabilities of PAM in this environment. Some Linux implementations also provide the pam_stack.so module that allows all authentication to be configured in a single central file. The pam_stack.so method has some devoted followers on the basis that it allows for easier administration. As with all issues in life, though, every decision has trade-offs, so you may want to examine the PAM documentation for further helpful information.

# 27.2.3 **smb.conf PAM Configuration**

There is an option in **smb.conf** called *obey pam restrictions*. The following is from the online help for this option in SWAT:

When Samba is configured to enable PAM support (i.e., --with-pam), this parameter will control whether or not Samba should obey PAM's account and session management directives. The default behavior is to use PAM for clear-text authentication only and to ignore any account or session management. Samba always ignores PAM for authentication in the case of *encrypt passwords* = yes. The reason is that PAM modules cannot support the challenge/response authentication mechanism needed in the presence of SMB password encryption.

Default: *obey pam restrictions* = no

# 27.2.4 **Remote CIFS Authentication Using winbindd.so**

All operating systems depend on the provision of user credentials acceptable to the platform. UNIX requires the provision of a user identifier (UID) as well as a group identifier (GID). These are both simple integer numbers that are obtained from a password backend such as /etc/passwd.

Users and groups on a Windows NT server are assigned a relative ID (RID) which is unique for the domain when the user or group is created. To convert the Windows NT user or group into a UNIX user or group, a mapping between RIDs and UNIX user and group IDs is required. This is one of the jobs that winbind performs.

As winbind users and groups are resolved from a server, user and group IDs are allocated from a specified range. This is done on a first come, first served basis, although all existing users and groups will be mapped as soon as a client performs a user or group enumeration command. The allocated UNIX IDs are stored in a database file under the Samba lock directory and will be remembered.