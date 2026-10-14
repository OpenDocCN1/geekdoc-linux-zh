The panic-action setting allows Samba to run a script when it crashes. The panic-action script is a canned script that sends information to the system administrator account of the Ubuntu server, providing basic information about the system crash.

# Authentication

The authentication section determines how user accounts are validated for access to the Samba server:

```
# security = user
encrypt passwords = true
passdb backend = tdb sam
obey pam restrictions = yes
unix password sync = yes
passwd program = /usr/bin/passwd %u
passwd chat = *Enter\snew\spassword:* %n\n *Retype\snew\spassword:* %n\n *password\ssuceeded\ssuccessfully*"
pam password change = yes
map to guest = bad user
```

These are very important parameters. They control how the Samba server authenticates users who request access to the server. User authentication can be done in three different ways:

+   User
+   Share
+   Domain

With the security parameter set to user (the default value since Samba 2.0), the Samba server will try to validate the requesting user by an existing Ubuntu system userID. If it's found, the user then has access to shares as determined by the standard Ubuntu file permissions for that userID (unless specifically restricted by the share section).

With the security parameter set to share, the Samba server attempts to authenticate users based on individual shared resources on the server. This setting is commonly used on Windows workstations that share folders by setting a password. Samba uses the standard Ubuntu system userID/password combination just as it does with the user security method.

By setting the security parameter to domain, Samba will try to find a domain controller to validate the userID and password. If the domain controller authenticates the userID and password, Samba grants access to the user connection.