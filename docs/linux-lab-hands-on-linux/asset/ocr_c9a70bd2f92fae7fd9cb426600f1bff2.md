```
#useradd Mahendra
```

This adds a new entry in /etc/passwd file. By default, this file stores all user account related information.

There is no default password for the previously created user Mahendra. In order to create a password for this user, you just need to type the passwd command on the command line as follows:

```
#passwd Mahendra
```

This will prompt you to enter a password. Enter the password and press enter. You will be asked to confirm the password. Type the password again and press enter. As long as you typed the same password in both times, you have finished adding a new user. If you did not enter the same password both times, you will be asked to reenter the password again until you confirm it correctly.

+   CASE 1: Let's take an example where you have a group of users from an IT department.
+   They regularly use a spreadsheet application on a system. You could create a new group called finance and make it the default group for spreadsheets. To create a group, run the following groupadd command:

```
#groupadd finance
```

Now, if you need to create a spreadsheet user named mahendra, you could use the following command:

```
#useradd Mahendra -g finance
```

This command creates a user named mahendra with a default group of finance.

If existing users need to be placed in the IT group, you could run the following command:

```
chgrp deven IT
```

It would make the IT group deven's new default group. If you need to make a particular user a member of more than one group at a time, use the -G option with the useradd command:

```
useradd mahendra -G IT, finance
```

The preceding command creates the user mahendra with a default group of Mahendra. At the same time, this user also becomes a member of the groups IT and finance. To see the existing groups and the members, run the following command:

```
#cat /etc/group
```

The etc/group file have four segments (group name:password:group ID:users) that are separated by colons. By seeing this file you can find the groups to whom Mahendra belong.