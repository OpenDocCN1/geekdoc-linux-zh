# Mail

Creating a new user means not only creating the user’s home directory and setting up the environment. It also means making it possible for the user to send and receive e-mail. Setting up a mailbox under Linux is quite easy, and if you use the tools that come with Linux to create the account, you don’t even have to do this yourself!

Mailboxes are kept in the /var/spool/mail directory. Each user has a mailbox that is based on his or her login name. Thus, if a user’s login is **bwoodall**, his mailbox will be /var/spool/mail/**bwoodall**. All mailboxes should be owned by their respective owners with the permissions set such that others cannot read its contents. (See the **chown**, **chmod**, and **chgrp** commands in Module 6 for details on how to do this.)

An empty mailbox is a zero-length file. To create a zero-length file anywhere in the system, you simply use the **touch** command like so:

```
```
[root@redford /root]#  touch myfile
```
```

This will create a new file called **myfile** in the current directory.

![](bbox=[0.09, 0.48, 0.18, 0.53])

# Progress Check

+   1. What is the usual location for user home directories?
+   2. What was the original encryption scheme used for passwords?
+   3. Name a BASH shell configuration filename.
+   4. Where would you expect to find user **mpawlowski**’s mailbox?

![](bbox=[0.08, 0.7, 0.15, 0.74])

# Managing User Databases

If you’re already used to Windows 2000 or .NET Server user management, you’re familiar with the Active Directory tool that takes care of the nitty-gritty details of the user database. This tool is convenient, but it makes developing your own administrative tools trickier, since the only other way to read or manipulate user information is through a series of LDAP calls.

+   1. The usual location for user home directories is /home.
+   2. The Data Encryption Standard (DES) was originally used for encrypting passwords.
+   3. The .bashrc file is a BASH configuration file (as is /etc/profile, although the latter isn’t covered here).
+   4. You would find **mpawlowski**’s mailbox at /var/spool/mail/**mpawlowski**.