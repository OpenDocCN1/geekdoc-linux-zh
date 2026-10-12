![](bbox=[0.04, 0.15, 0.14, 0.25])

# ## Shadow passwords

Instead of storing the passwords in the /etc/passwd file, which any user can read, passwords are now stored in a shadow password file. On Red Hat Linux, the shadow passwords are in the /etc/shadow file. Only the super user (root) can read this file. For example, here is the entry for root in the new-style /etc/passwd file:

```
root:x:0:0:root:/root:/bin/bash
```

As you can see, the second field contains an x instead of an encrypted password. The encrypted password is now stored in the /etc/shadow file where the entry for root is like this:

```
root: $1 $ AAAAA r / y b W 5 t E 8 H b z U p 9 c f o o l P f 8 1 0 S 0 : 1 0 7 7 : 0 : 9 9 9 9 9 : 7 : - 1 : 1 3 4 5 4 3 4 0 3 5 6
```

The format of the /etc/shadow entry control when the password expires. You do not need to interpret or change these entries in the /etc/shadow file. Instead, you should use the chage command to change the password expiration information. For starters, you can check a user's password expiration information by using the chage command with the -1 option as follows (in this case, you have to be logged in as root):

```
change -l root 
 Minimum: 0 
 Maximum: 99999 
 Warning: 7 
 Last Change: -1 
 Password Expires: Never 
 Password Inactive: Never 
 Account Expires: Never
```

In this case, the output shows various expiration information: you can change the root password any time—that's what zero minimum time means. The root password lasts for 99,999 days, and the root user gets a warning seven days before the password expires.

If you want to ensure that the password changes every 90 days, you can use chage's -M option to set the maximum number of days the password stays valid. For example, to make sure that user kwall is prompted to change the password in 90 days, you would log in as root and type the following command:

```
chage -M 90 kwall
```

You can do this for each user account to ensure that all passwords expire and all users must pick new passwords.

# ## Pluggable Authentication Modules

In addition to improving the password file's security by using the shadow passwords, Red Hat Linux also enhances the actual encryption of the passwords stored in the /etc/shadow file. Password encryption is now done using the MD5 message-digest algorithm to convert