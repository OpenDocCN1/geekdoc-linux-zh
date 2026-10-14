Figure 9-10 shows the entry for the user geeko with an encrypted password. The plain text password is novel1.

The encrypted password is coded with the Blowfish algorithm. The encrypted word consists of letters, digits, and some special characters. If an invalid character (such as “*” or “!”) occurs in the Password field, that user has an invalid password.

Many users, such as wwwrun (Apache Web server) or bin have an asterisk (“*”) in the Password field. This means that these users cannot log in to the system, but are needed for special applications.

If the Password field is empty, then the user can log in to the system without entering a password. A password should always be set in a Linux system.

The information at the end of each line determines some limits:

+   - *Last Change*—Date of last password change. The number represents the number of days since January 1, 1970.
+   - *Next Possible Change*—Minimum age of a password before a user can change it.
+   - *Next Obligatory Change*—Number of days a user can use the same password before it expires.
+   - *Warning*—Number of days users get a warning before password expiration. Enter −1 to disable the warning.
+   - *Limit*—Number of days after the password expires that the user can continue to log in. Enter −1 for unlimited access. (This does not make sense, of course.)
+   - *Lock*—Date when the account expires. The date must be in the format YYYY-MM-DD. Leave the field empty if the account never expires.

# **/etc/group**

The /etc/group file stores group information. The following is a sample /etc/group file.

```
at:!:25:
audio:x:17:
bin:x:1:daemon
cdrom:x:20:
console:x:21:
...
video:x:33:geeko
wheel:x:10:
www:x:8:
xok:x:41:
users:x:100:
```

Each line in the file represents a single group record, and contains the group name, the GID (Group ID), and the members of the group. For example, this is the entry for the group video in the /etc/group file:

```
video:x:33:geeko
```