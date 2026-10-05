# CHAPTER 2 Managing Local Users and Groups

+   The root user can set a password to any value. A message is displayed if the password does not meet the minimum criteria, is followed by a prompt to retype the new password and all tokens are updated successfully.

```
[root ~]# password user01
Changing password for user01.
New password: redhat
BAD PASSWORD: The password fails the dictionary check - it is based on a\dictionary word
Retype new password: redhat
passwd: all authentication tokens updated successfully.
[root ~]#
```

+   A regular user must choose a password at least eight characters long and is also not based on a
dictionary word, the username, or the previous password.

# UID Ranges

Specific UIDs and ranges of numbers are used for specific purposes by Red Hat Enterprise Linux.

+   * UID 0 is always assigned to the superuser account, root.

+   * UID 1-200 is a range of "system users" assigned statically to system processes by Red Hat.
file system. They are typically assigned dynamically from the available pool when the software
that needs them is installed. Programs run these as "unprivileged" system users in order to limit
tair access to the resources they need to function.

+   * UID 1000+ is the range available for assignment to regular users.

> NOTE
Prior to RHEL 7, the convention that UID 1-499 was used for system users and
UID 500+ for regular users. Default ranges used by useradd and groupadd can be
changed in the /etc/login.defs file.

> REFERENCES
useradd(8), usermod(8), userdel(8) man pages