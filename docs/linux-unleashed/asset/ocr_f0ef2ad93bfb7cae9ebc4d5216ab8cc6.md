To add an entry to the /etc/passwd file, use any editor that saves information in ASCII. Add the new users to the end of the file, using a new line for each user. Make sure you use a unique username and user ID (UID) for each user. For example, to add a new user called “bill” to the system with a UID of 103 (remember to keep UIDs sequential for convenience) and a GID of 100 (the default group), a home directory of /home/bill, and a startup shell of the Bourne shell, add the following line to the /etc/passwd file:

```
bill::103:100:Bill Smallwood:/home/bill:/bin/sh
```

Note that we have left the password blank because you can’t type in an encrypted password yourself. As soon as you have saved the changes to /etc/passwd, set a password for this account by running the following command:

```
passwd bill
```

This command prompts you for an initial password. Set the password to something that Bill will be able to use, and ask him to change the password the first time he works on the system. Many system administrators set the initial password to a generic string (such as “password” or the login name) and then force the new user to change the password the first time they log in. Using generic strings is usually acceptable if the user logs in quickly, but don’t leave accounts with generic login strings sitting around too long—someone else may use the account.

After you have added the necessary line to the /etc/passwd file, you should create the user’s home directory. Once created, you must set the ownership to make that user own the directory. For the preceding example, you would issue the following commands:

```
mkdir /home/bill
chown bill /home/bill
```

All users must belong to a group. If your system has only one group defined, then add the user’s username to the line in the /etc/group file that represents that group. If the new user should belong to several groups, add the username to each group in the /etc/group file. The /etc/group file and groups in general are discussed in the “Groups” section later in the chapter.

Finally, the configuration files for the users’ shells should be copied into their home directory and set to allow them access for customization. For example, if you copy the Bourne shell’s .profile file from another user called “yvonne,” you would issue the following commands:

```
cp /home/yvonne/.profile /home/bill/.profile
chown bill /home/bill/.profile
```