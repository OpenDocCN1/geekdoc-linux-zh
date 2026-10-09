```
[root@localhost ~]# passwd pat
Changing password for user pat.
New UNIX password:
Retype new UNIX password:
password: all authentication tokens updated successfully.
[root@localhost ~]#
```

Figure 2-3: Setting password for the user "pat."

![](bbox=[0.22, 0.28, 0.29, 0.34])

You can change the password of your user account using the `passwd` command. You cannot change the password for any other user account because the `passwd` command does not allow you to specify any other user name. Only the root user can change the password for other users by specifying the user name with the `passwd` command.

# Syntax

A root user can create a password for a user by entering `passwd [user_name]`, where `[user_name]` is the name of the user for whom the password is set.

# Bad Password Message

If you enter an alphanumeric password, you may get a bad password message stating that it is based on a dictionary word. The password will still be assigned even though the message is displayed. You will probably need to change it to a more secure password.

![](bbox=[0.03, 0.55, 0.11, 0.62])

The /etc/passwd File

# The /etc/passwd File

When you add a new user, information about the user is saved in the /etc/passwd file.

There are various fields in the /etc/passwd file.

| Field | Description |
| :--- | :--- |
| User name | Stores the user name with which the user logs in to the system. It is recommended to limit user names to eight alphanumeric characters. |
| Password | Stores the password that is assigned to the user in an encrypted form. |
| User ID | Stores the unique number that is assigned to each user. Linux tracks users by the UID rather than the user name. |
| Group ID | Stores the unique number that is assigned to each group. Users can be members of one or more groups. |
| Full name | Stores the real name of the user. |
| Home directory | Displays the default directory where the user is placed after logging in. |
| Login shell | Displays the default shell that is started when the user logs in. |