The ac command is most useful in shell scripts to generate reports on operating system usage for management review.

The last command searches through the /var/log/wtmp file and will list all the users logged in and out since that file was first created. The user reboot exists so that you might know who has logged in since the last reboot. A companion to last is the command lastb, which shows all failed, or bad, logins. It is useful for determining if a legitimate user is having trouble or if a hacker is attempting access.

> **NOTE**
> 
> The accounting system on your computer keeps track of usage user statistics and is kept in the current /var/log/wtmp file. That file is managed by the init and login processes. If you want to explore the depths of the accounting system, use the GNU info system: info accounting.

# # Managing Passwords

Passwords are an integral part of Linux security, and they are the most visible part to the user. In this section, you will learn how to establish a minimal password policy for your system, where the passwords are stored, and how to manage passwords for your users.

# ## System Password Policy

An effective password policy is a fundamental part of a good system administration plan. The policy should cover:

+   * Allowed and forbidden passwords
+   * The frequency of mandated password changes
+   * The retrieval or replacement of lost or forgotten passwords
+   * Password handling by users

# ## The Password File

The password file is /etc/passwd, and it is the database file for all users on the system. The format of each line is as follows:

```
username:password:uid:gid:gecos:homeDir:shell
```

The fields are self-explanatory except for the GECOS field. This field is for miscellaneous information about the user, such as the users' full name, his office location, office and home phone numbers, and possibly a brief text message. For security and privacy reasons, this field is little used nowadays, but the system administrator should be aware of its existence since the GECOS field is used by traditional Unix programs such as finger and mail. For that reason, it is commonly referred to as the *finger information field*. The data in this field will be comma delimited; the GECOS field can be changed with the cgf/n (change finger) command.