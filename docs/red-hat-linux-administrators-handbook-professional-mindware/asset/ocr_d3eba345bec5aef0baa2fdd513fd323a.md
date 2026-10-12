**Table 15-1 Fields in the /etc/shadow File**

| Fields | Description |
|---|---|
| *username* | The username |
| *passwd* | The encrypted character password |
| *last* | Date of last password change |
| *min* | Minimum number of days after which the current password may be changed |
| *max* | Maximum number of days after which the current password must be changed |
| *warn* | Number of days after which the user will be warned about the current password becoming expired |
| *expire* | Number of days after which the current password expires and the account is disabled |
| *disable* | Number of days since the account has expired |

The new fields (everything but the *username* and *passwd*) can be used to provide the user accounting functionality, such as account expiration and password aging. The */usr/sbin/pwconv* utility uses the *PASS_MAX_DAYS* (maximum number of days after which the current password must be changed), *PASS_MIN_DAYS* (minimum number of days after which the current password may be changed), and *PASS_WARN_AGE* (number of days after which the user will be warned about the current password becoming expired) values from */etc/login.defs* file. Modify the */etc/login.defs* file to set desirable values for these fields.

# ### Managing user accounts

The shadow utility package installs replacements for utilities such as useradd, userdel, usermod, groupadd, groupdel, and groupmod, which typically are used to manage user accounts. You can run the following *rpm* command to find out what actually got copied when you installed this package:

```
```
rpm -q -l shadow-utils-version-release
```
```

Replace *version-release* with actual version and release information from your copy of the shadow utility package.

The new and increasingly popular *linuxconf* utility is also capable of working with shadow password systems. This dialog box becomes part of the user account creation process and allows you to specify information