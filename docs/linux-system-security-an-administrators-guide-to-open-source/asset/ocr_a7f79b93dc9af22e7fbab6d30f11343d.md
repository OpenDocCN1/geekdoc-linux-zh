Consider another example. Suppose that we want to limit the users to which others may *su*—we want to restrict *su* use generally (not just *su* to root) to a specific set of users. We add a pam_listfile entry to `/etc/ pam.d/su` as displayed in Example 5-18. This time we are using an allow list. Just place each allowed username, one per line, in the `/etc/ security/suok` file. For example, if our `/etc/ security/suok` contains the users:

root
mary
bill
Jane
efram

then these are the only users that will be accepted as a user argument to *su*. Anyone may execute *su*, but only to become one of the users in this list. Example 5-19 shows what happens when *paul* tries to *su* to *guest* and then to *root*. The *su* attempt to *guest* fails because *guest* is not in the `/etc/security/suok` file. The *su* to root, however, succeeds because *root* is in the `/etc/security/ suok` file and *Paul* knows the root password.

# Example 5-18  The *su* Configuration File with pam_listfile

| auth    | required  | /lib/security/pam_listfile.so onerr=fail \
|         |           |     item=user  sense=allow  file=/etc/security/suok | |
| auth    | required  | /lib/security/pam_pwdb.so |
| account | required  | /lib/security/pam_pwdb.so |
| password| required  | /lib/security/pam_cracklib.so minlen=20 retry=3 |
| password| required  | /lib/security/pam_pwdb.so md5 use_authtok |
| session | required  | /lib/security/pam_pwdb.so |

# Example 5-19  Failed *su* Attempts Due to pam_listfile

```
```
$ whoami
joe
$ su - guest
Password:
su:  incorrect password
$ su -
Password:
# ```
```

Notice that the error message is not indicative of the actual failure. If you review the previous failure messages from other PAM modules, you'll see that this is a feature of PAM. The idea is to not reveal any information to the user through error messages. As an administrator with root access, you may always check out the log files. By default, you will find PAM-generated log messages in `/var/log/messages` (these files and *syslog*, in general, will be dis- cussed in Chapter 8).

Note that when *sense=allow* changes to *sense=deny* in Example 5-18, the `/etc/security/suok` file becomes a deny list, meaning that a user would not be able to *su* to any of the users in the list. This is particularly useful if you wish to implement *sudo* (*sudo* is discussed in Chapter 9) and completely disallow *su* to root.