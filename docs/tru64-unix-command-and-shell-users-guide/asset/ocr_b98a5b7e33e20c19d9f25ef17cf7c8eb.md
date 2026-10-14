/etc/passwd　　 This file contains individual user information for all users of the system.

/etc/group　　 This file contains group information for all groups on the system.

These files define who can use the system and each user’s access rights. In addition, all other system security controls depend upon password and group security. The following sections describe the `/etc/passwd` and `/etc/group` files.

# 5.1.1 The /etc/passwd File

The `/etc/passwd` file contains records that define login accounts and attributes for all system users. This file can be altered only by a user with **superuser** privileges. See Section 5.7 for more information.

Each record in the `/etc/passwd` file defines a login account for an individual user. The fields are separated by colons and the last field ends with a newline character. The following text shows the format of an `/etc/passwd` file entry and describes the meaning of each field:

```
username:password:UID:GID:gecos:login_directory:login_shell
```

+   - **username** — Your login name.
+   - **password** — Your password stored in encrypted form. Encryption prevents unauthorized users or programs from discovering your actual password. If no password has been specified for a user, this field will be blank.
+   - **UID** — (User ID) A unique number identifying you to the system.
+   - **GID** — (Group ID) A number identifying your default group. You can belong to one or more groups.
+   - **gecos** — This field usually contains general information about you, stored in some installation specific format. Historically, this is a comma separated list of the following:
+     - **name** — Your full name