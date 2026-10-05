
## Deleting Accounts

- It moves the contents of the account's original home directory to its new location.

You might issue a command like this one if you were migrating user accounts to an NFS server mounted at /home2. Such a change might require a new home directory location and a change in the UID value to match the one used on the NFS server.

You should be careful when making changes to the UID value because, although usermod changes the UID values of files in common locations such as the user's home directory and email files, it can miss users in unusual locations.

If you need to make group changes that require adding new groups, consult the upcoming section, “Managing Groups,” for information on that topic.

## Deleting Accounts

Deleting accounts can sometimes be as important as adding or modifying them. Unused accounts can be abused, either by their former owners or by others who might be able to break into an account if it has a weak password. Thus you should routinely delete unused accounts. Before you do so, though, you should understand what happens when you delete an account and decide precisely how to do it, let create problems by deleting an account in an inappropriate way. With that knowledge in hand, you can delete accounts using any GUI or text-mode tools.

> --move-home (-m) option will be quick when the move is on a single low-level filesystem but potentially slow when it crosses filesystem boundaries.

> Consider archiving a deleted account's home directory to a long-term backup medium. This will enable you to recover the files if they become valuable in the future.

## Avoiding Account-Deletion Pitfalls

An account may sound simple enough, but a mistake can cause problems, either immediately or in the future. To avoid obvious issues such as accidentally deleting the wrong account, you should consider two factors:

### User File Preservation
Users' files may be extremely valuable, either to the users themselves or the organization that owns the computer. You should check your company's file retention policies when considering whether to delete the user's home directory or do something else with it, as move it into another user's home directory and change permissions on the files it contains. The same is true of the user's mail queue (normally stored in /var/spool/mail/username, where username is the username).

# Chapter 13 · Creating Users and Groups

### UID and GID Reuse
When an account is deleted, the account's UID and GID become available for reuse. In many cases, these numbers will not be reused, since Linux assigns these values based on the highest current value. Thus if you delete any the highest-numbered current user won't be reused unless intervening accounts are also deleted. Nevertheless, if a UID is reused, previously owned by the old user will suddenly appear to be owned by the new user. This might not cause any problems, but it might cause confusion about who created the files. In some cases, it could even cause suspicion of wrongdoing by the new user (if the old files contain information the new user doesn't have, or if they reside in directories to which the new user shouldn't have access).

If you want to avoid any chance of confusion or misbehavior claims facing new users due to UID or GID reuse, you can use the find command in Chapter 8 "Searching, Extracting, and Archiving Data" to locate all files with particular UID or GID values, using the -uid and -gid options, as in:

```
# find -uid 1004
```

This example finds all files on the computer with a UID of 1004. (Searching on a GID works the same way, but using the -gid option.) You can then reassign ownership of these files by using the ch command (covered in Chapter 14) or delete them. Ordinarily, you'd issue this command only after deleting or reassigning ownership of the user's home directory, since that directory will probably contain far too many files.

## Deleting Accounts Using GUI Tools

With other account management tasks, using a GUI is fairly intuitive, but details vary from one distribution to another. As an example, to delete an account from openSUSE's User and Group Administration utility, after you have the utility open, you should click the account and then click the Delete button. The result is a confirmation dialog box similar to the one shown in Figure 13.5. Check or uncheck the box to delete the user's home directory as you see fit and, and if you're certain of the action, click the Yes button. The account will be immediately deleted.

If the user is currently logged in, the utility will typically complain about this fact in the confirmation dialog box. You'll still be able to delete the account, but the user won't be logged out immediately.

![](img/77662199428609b7662c8dc9c0e45c10_281_0.png)

## Deleting Accounts

![](img/77662199428609b7662c8dc9c0e45c10_282_0.png)

FIGURE 13.5: When you delete an account with a GUI utility, you may be able to optionally delete the user's home directory.

## Deleting Accounts from the Shell

The userdel command deletes accounts from a text-mode shell. In its simplest form, you pass it a username and nothing more:

```
$ sudo userdel samantha
root's password:
```

The program does not prompt you for confirmation; it just deletes the account. It does not, however, delete the user's home directory by default. If you have to do so, pass it the remove (-r) option.

If the user is currently logged in, userdel notifies you of that fact and does nothing. You can pass the --force (-f) option to delete the account even though it's logged in. To both force account deletion and remove the user's files, you can pass both options:

```
$ sudo userdel -rf samantha
root's password:
userdel: user samantha is currently logged in
```

The program still complains about the user being logged in, but it deletes the account and files just the same.

> Notice that if the user has many files, and you opt to delete those files, the deletion operation may take several seconds, or even minutes, to complete.

# Chapter 13 · Creating Users and Groups

## Managing Groups

In many respects, groups are comparable to accounts. They are defined in similar files and managed with similar utilities. Groups are also tied to accounts, in that accounts include group definitions. Until now, it has been assumed that you'll be using standard groups or the groups that are defined as part of account creation. Sometimes, though, need to create, delete, or modify groups for specific purposes, as if you use project group strategy. With account management, you can do this using either GUI or text-mode tools.

### Managing Groups Using GUI Tools

Many account maintenance tools, such as openSUSE's User and Group Administration utility, provide group management tools that are similar to the user management described throughout this chapter. Referring back to Figure 13.1, you will see that the User and Group Administration window includes both Users and Groups tabs. To manage groups, click the Groups tab. This produces a display resembling Figure 13.6.

![](img/77662199428609b7662c8dc9c0e45c10_283_0.png)

FIGURE 13.6: The User and Group Administration utility enables you to manage groups as well as users.

You can add, modify, and delete groups in a manner that's comparable to adding, modifying, and deleting accounts, though the number of options available may be much smaller. Groups don't have home directories, comment fields, login shells, and so on. You might, of course, want specific users to be members of your new group from the start. To do so, follow these steps:

- 1. Create a group by clicking the Add button within the Group tab.
- 2. Specify the group name and GID in the resulting dialog box.
- 3. Add group members by pressing a check mark (in the box) next to the account name, as shown in Figure 13.7.

![](img/77662199428609b7662c8dc9c0e45c10_284_0.png)

FIGURE 13.7: You can add users to a group when creating the group.

- 4. Complete the group's addition by clicking the OK button.

Alternatively, you can manage group membership by altering each user's group membership individually, as described next in “Managing Groups from the Shell.”

### Managing Groups from the Shell

You can create groups from the shell by using the groupadd command, which works much like user for users but takes a smaller set of options, the most important of which appear in Table 13.3. Consult the program's man pages for information on more-obscure options.
