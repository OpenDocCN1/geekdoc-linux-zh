# SETTING UP A SAMBA Server

The username that is assigned to users logging in as guest or mapped to guest; apply only when guest ok (page 813) is set to YES. This username should be present in /etc/passwd but should not be able to log in on the system. Typically guest account is assigned a value of nobody because the user cannot access only files that any user can access. If you are using the nobody account for other purposes on the Linux system, set this parameter to a other name than nobody.

Default: nobody

Analogous to the /etc/hosts.allow file (page 465); specifies hosts that are allowed to connect to the server. Overrides hosts specified in hosts deny. A good strategy is to specify ALL hosts in deny and to specify the hosts you want to grant access to in this file. Specify hosts in the same manner as hosts.allow.

Default: none (all hosts permitted)

Analogous to the /etc/hosts.deny file (page 465); specifies hosts that are not allowed to connect to the server. Overridden by hosts specified in hosts allow. If you specify ALL in this file, remember to include the local system (127.0.0.1) in hosts allow. Specify hosts in the same manner as hosts.deny.

Default: none (no hosts excluded)

Lists users who are not allowed to log in Samba.

Default: none (all users are permitted to log in)

Ubuntu: (all users are permitted to log in)

Defines when a failed login is mapped to the guest account. Useful when we security (page 810) is not set to SHARE.

Never: Allows guest to log in only when the user explicitly provides guest as the username and a blank password.

Bad: Treats any attempt to log in as a user who does not exist as a guest login. This parameter is a security risk because it allows a malicious user to retrieve a list of users on the system quickly.

Bad Password: Silently logs in guest as user who incorrectly enters her password. This parameter may confuse a user when she mistypes her password and is unknowingly logged in guest because she will suddenly see fewer shares than she is used to.

Default: Never

Ubuntu: Bad User

Specifies what Samba stores passwords. Set to ldapsam for LDAP, smbpasswd for Samba, or tdbsam (trivial database) password storage. See page 803 for instructions on using smbpasswd to change Samba passwords.

Default: smbpasswd

Ubuntu: tdbsam