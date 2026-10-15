framework that supports all sorts of standard authentication services, including LDAP and NIS.

# Basic file sharing

If each user has a home directory, the homes can be "bulk shared":

```
[homes]
comment = Home Directories
browseable = no
valid users = %S
writable = yes
guest ok = no
```

This configuration allows the user oetiker (for example) to access his home directory through the path \\sambaserver\oetiker from any Windows system.

At some sites, the default permissions on home directories allow people to browse one another's files. Because Samba relies on UNIX file permissions to implement access restrictions, Windows users coming in through CIFS can read one another's home directories as well. However, experience shows that this behavior tends to confuse Windows users and make them feel exposed. The valid users line in the configuration fragment above tells Samba to prevent connections to other people's home directories. Leave it out if this is not what you want.

Samba uses its magic [homes] section as a last resort. If there is an explicitly defined share in the configuration for a particular user's home directory, the parameters set there override the values set through [homes].

# Group shares

Samba can map Windows access control lists (ACLs) to either file permissions or ACLs (if the underlying filesystem supports them). In practice, we find that the concept of ACLs tends to be too complex for most users. Therefore, we normally just set up a special share for each group of users that requires one and configure Samba to take care of setting the appropriate permissions. Whenever a user tries to mount this share, Samba checks to make sure the applicant is in the appropriate UNIX group and then switches its effective UID to the designated owner of the group share (a pseudo-user created for this purpose). For example:

```
[eng]
comment = Group Share for engineering
; Everybody who is in the eng group may access this share.
; People will have to log in using their Samba account.
valid users = @eng
; We have created a special user account called "eng". All files
; written in this directory will belong to this account as
; well as to the eng group.
force user = eng
force group = eng
path = /home/eng
```