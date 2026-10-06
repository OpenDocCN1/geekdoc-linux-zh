# TABLE 10.1 User Account Parameters

| Parameter | Description |
|---|---|
| The account is enabled | If checked, the user can log in. |
| Login name | The login name of the user account. The login name should not contain special characters other than dash (-) or underscore (_). The login name can be many as 256 characters in length; however, most system administrators assign login name of not more than 8-10 characters in length. |
| Full name | The user's full name (optional). |
| Group | The numeric ID of user's home group (optional). By default, a personal group having the same name as the login is created. |
| Supplementary groups | Additional groups to which the user belongs (optional). By default, no additional groups are assigned. |
| Home directory | The user's home directory (optional). By default, the *directory/home/login_name* is assigned, where *login_name* is the user's login name. |
| Command interpreter | The command interpreter (shell), /bin/bash by default (optional). |
| User ID | The numeric user ID (optional). By default, the next sequential numeric ID is assigned. |
| Must keep # days | Number of days the user must keep the password, or -1 if the password can be changed immediately. |
| Must change after # days | Number of days until the user must change the password, or 99999 if the password does not expire. |
| Warn # days before expiration | Number of days given before password expiration, or -1 if no warning is to be given. |