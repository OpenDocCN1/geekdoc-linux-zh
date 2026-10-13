
To make life a little easier, the **useradd** command also supports the **-D** command-line argument, which enables you to assign default values to authorizations (**-A**), the base directory (**-b**), the group (**-g**), the expiration date (**-e**), the maximum inactivity (**-f**), execution profiles (**-P**), and roles (**-R**). Subsequent uses of the **useradd** command will use these default values if they are not specified, as shown in this example:

```
# useradd -D -b /export/home -g other
 group=other, proj=3  basedir=/export/home
 skel=/etc/skel  shell=/bin/sh  inactive=0
 expire=  auths=  profiles=  roles=
#
# useradd -m -u 1051 user2
6 blocks
#
```

Because a default base and group were defined, the user2 account is a member of the group other and has a home directory of /export/home/user2.

![](img/b957f979417d9f16274c2eb52c8f2c9f_155_0.png)

> User accounts created with the useradd command do not have a password. These accounts are locked and cannot be used until a password is defined for the account by using the passwd(1) command.

## Modifying an Account by Using the usermod Command

The usermod(1M) command is used to modify an existing user account. The command-line arguments are identical to the useradd command-line arguments, with the following exceptions:

- The base directory (**-b**) is not available. Use **-d** to specify a new directory. Don't forget to include **-m** if the specified directory doesn't exist.
- Set defaults (**-D**) is not available.
- The template directory (**-k**) is not available.
- You specify a new user account name by using **-l account** if the account name is being modified.

Keep in mind that if the account name is changed, the name of the home directory does not change unless you use the **-d** and **-m** command-line arguments. The following example uses the **usermod** command to change the name of the user1 account to user3:

```
# ls -l
total 22
drwx------  2 root   root     8192 Jan 13 21:05 lost+found
drwxr-x---  2 user1  other     512 Mar 31 13:23 user1
drwxr-x--  2 user2  other     512 Mar 31 13:45 user2
#
# usermod -l user3 -d /export/home/user3 -m user1
6 blocks
#
# ls -l
 total 22
drwxr-x--x  2 user2 other 512 Mar 31 13:45 user2
drwxr-x--x  2 user3 other 512 Mar 31 13:23 user3
#
```

## Deleting an Account by Using the userdel Command

The userdel(1M) command is used to delete a user account. You specify the user account as a command-line argument. Only one other command-line argument, **-r**, is supported—it’s used to remove the home directory:

```
# userdel -r user3
#
```

## Group Accounts

You can add, modify, or delete group accounts by using command-line utilities or the admintool(1M) command. Using the admintool command reduces or eliminates the possible introduction of typos and other errors that might affect all group accounts.

These are the command-line utilities:

- **groupadd**(1M)
- **groupmod**(1M)
- **groupdel**(1M)

Both the admintool command and the command-line utilities are described in the following sections.

### Creating a Group by Using the admintool Command

To create a group account, start the admintool command if it is not already active, and then choose Browse, Groups from the menu to open the Groups dialog box (see Figure 6.4).

Then open the Add Group dialog box, shown in Figure 6.5, by choosing Edit, Add from the menu.

![](img/b957f979417d9f16274c2eb52c8f2c9f_157_0.png)

**Figure 6.4** The Admintool: Groups dialog box.

![](img/b957f979417d9f16274c2eb52c8f2c9f_157_1.png)

**Figure 6.5** The Admintool: Add Group dialog box.

Enter a unique group name in the Group Name field. Use the next available GID number or enter a unique GID in the Group ID field. In the Members List field, enter one or more user account names separated by commas. Click OK, and the new group is displayed in the Groups dialog box.

### Modifying a Group by Using the **admintool** Command

To modify a group account, start the **admintool** command if it is not already active, and choose Browse, Groups from the menu. Click the account entry to highlight it, and then choose Edit, Modify from the menu to open the Modify Group dialog box, which is similar to the Add Group dialog box (shown previously in Figure 6.5). The fields are filled in with information about the selected group. Change the fields as needed and click Apply to save the changes.

### Deleting a Group by Using the **admintool** Command

To delete a group account, start the **admintool** command if it is not already active, and choose Browse, Groups from the menu. Click the account entry to highlight it, and then choose Edit, Delete from the menu. A Warning dialog box similar to the one shown previously in Figure 6.3 opens, but it lists a group instead of a user. Click Delete to delete the group account.

![](img/b957f979417d9f16274c2eb52c8f2c9f_158_0.png)

Because using the **admintool** command makes creating, modifying, and deleting group accounts easy, Exam CX-310-011 concentrates on using the **groupadd**, **groupmod**, and **groupdel** commands for administering group accounts.

### Creating a Group by Using the groupadd Command

The **groupadd**(1M) command provides a quick method to add a new group account. At a minimum, you must specify the group account name as a command-line argument. The **groupadd** command supports two other command-line arguments. The first is **-g gid**, which specifies the unique GID that should be associated with the group. It must be a decimal integer. If you don’t specify a GID, the next highest available GID is assigned. The other command-line argument is **-o**, which lets you assign a duplicate GID to the group.

The following example creates a group by using the **groupadd** command:

```
# groupadd -g 1000 newgroup
#
```

### Modifying a Group by Using the groupmod Command

The **groupmod**(1M) command is used to modify an existing group account. The command-line arguments are identical to the **groupadd** command-line arguments, except that you specify the new group account name by using **-n name** if the group account name is being modified. The following example uses groupmod to change the group newgroup to group:

```
# groupmod -n group newgroup
#
```

### Deleting a Group by Using the groupdel Command

The **groupdel**(1M) command is used to delete a group account. The group account is specified as a command-line argument:

```
# groupdel group
#
```

## Password Administration

Password administration involves setting parameters to control password aging, changing a user’s password as needed, and possibly locking a user account to prevent its use.

### Password Aging

The parameters of the /etc/shadow file, which you set through the Account Security fields of the **admintool** command’s Add or Modify User dialog box, determine the password aging policy. These parameters include how long a password is valid (Max Change), how often it can be changed (Min Change), and how long an account can be inactive before the password must be changed (Max Inactive). They enforce a policy for protecting password integrity.

Note that only Max Inactive can be specified by using the **useradd** command and modified by using the **usermod** command.

### Password Requirements

Unless specified by a superuser account such as root, passwords must meet the following requirements:

- A password must contain at least the number of characters specified by the PASSLENGTH parameter in the /etc/default/passwd file. The default is six; the recommended is eight or more.
- A password must contain at least two alphabetic characters and at least one numeric character (within the first PASSLENGTH characters).
- A password cannot be the same as the user account name, the reverse of the user account name, or a circular shift of the user account name. Any uppercase letters are mapped to lowercase letters for requirement checking. As a result, the password for the guest user account cannot be guest, tseug, uestg, estgu, GUEST1, and so on.
- A new password must differ by at least three characters from the old password. Again, uppercase and lowercase letters are equivalent for requirement checking.

![](img/b957f979417d9f16274c2eb52c8f2c9f_159_0.png)

Passwords can be any length, but only the first eight characters are significant. For example, if a password is defined as **25administration**, 25admini can be used to log in to the system.

Keep in mind that these requirements do not apply when root or some other superuser account defines its own password or the password of another user account.
