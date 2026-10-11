
## Password Entry

Not all groups require password entries. A password is for those who might try to use the `chgrp` command to change to a different group than they are by default. Any group that people should not be able to change into without authentication should have a password set. As with the `/etc/shadow` file, the password listed in `/etc/group` is encrypted. And if you are using the shadow suite, this password will only be an "x" and the real password is stored in `/etc/gshadow`. See Chapter 20 for more information on the shadow suite.

| Related solution: | Found on page: |
| :--- | :--- |
| Activating And Deactivating The Shadow Suite | 264 |

## UID List

Notice that the UID portion of the sample `/etc/group` listing is blank. Users that are explicitly assigned to a group in `/etc/passwd` do not need to be assigned in `/etc/group` as well. However, `/etc/passwd` only allows you to assign only one group to a user. If you want to add a user to any additional groups you must do so in `/etc/group`.

To add more than one user to a group, use the format "user1,user2,user3" and so on.

## Create The User's Home Directory

The `useradd` program also creates a home directory for the user. By default, this home directory is created as `/home/loginname`. Once this directory is created, the proper permissions and ownerships are set for it. The permissions on a shell user's home directory are `rwx------`, so that only the user who owns the directory can access it—`rwx------` only gives access to the owner of the directory, no one else aside from root can get in (permissions are discussed in detail in Chapter 3). The user and group ownerships in Red Hat Linux's default `useradd` setup are both set to the same thing—the identical user and group names. For example, when doing a listing of the user dog's home directory, the list might look like what is shown in Figure 2.1.

## Set Up The User's Default Files

Finally, the `useradd` program goes to a skeleton user directory stored in the directory `/etc/skel`. Within this directory are the login settings and scripts that need to go into a new user's directory. All files are as generic as possible, using environment variables like `$HOME` for a home directory instead of an absolute path. (Environment variables and shell scripting are covered in Chapter 20—these files will make more sense then.) Everything within the skeleton directory goes into every new shell account home directory.

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_57_0.png)

Figure 2.1 A long form listing of the user dog's home directory from within the home hierarchy.

## Analysis Of The userdel Process

When you delete a user account by using the command line program **userdel**, it is important to understand what this program does and does not do. It takes care of most of the user removal process for you but not all of it. If you want to completely remove a user account from the system, you will have to do some extra work.

### Remove The User Entry From Files

First, the **userdel** program removes the user account from the user management files. This action prevents the user from being able to log in, and it prevents any-one from being able to change to the user's personal group. To accomplish this task, the **userdel** program opens the /etc/passwd file and removes the user's entry there, then the /etc/shadow file, if it exists, is opened and the entry is removed from there as well (more on the shadow suite in Chapter 9). The account removal tool then does the same in /etc/group, removing the user's personal group and also removing the account from any other groups. (If you are using shadow groups, the program also goes into /etc/gshadow (see Chapter 9 for more on shadow groups).

### Remove The Files

Once the user entries are removed from the user management files, **userdel** turns to the account's home directory and deletes it. However, this is all it deletes. The user may have programs or files installed elsewhere. Items may exist in the /tmp directory, /usr/sbin, or other locations the user might have had access to, such as /var/spool/mail where mail spools are kept (more on email in Chapter 12). See the section “Removing Users” in the Immediate Solutions section for instructions on how to make sure that legacy files are not left behind.

## Clever Uses For Groups

Many people seem to forget completely that groups exist. This fact is a shame. There are facets to using groups that can make your life as a system administrator easier and your file system more secure.

### Group Storage

A good use for user groups is to create them for project teams. Each member of these teams tends to need access to the same set of materials, such as project guidelines, data, and documents. Creating either a separate partition or a section in the main file system for team files to reside on reduces the need for excessive use of symbolic links between user directories.

Furthermore, with tools like Network File System (NFS) and Samba at your fingertips, group file storage areas can be made network accessible.

| Related solutions: | Found on page: |
| :--- | :--- |
| Setting Up NFS Exports | 505 |
| Mounting Remote File Systems With NFS | 505 |
| Building A File Share Statement | 541 |
| Mounting Windows Shares Under Linux | 546 |

### Group Access

Sometimes the need to utilize groups creatively is more one of access to scattered programs or special areas of the regular file system than just grouping users. For example, the accounting department may need access to specific programs on its company’s main server. Levels of administrative access can also be made using this function. For example, you can make an access level called “webmaster” below root that has access to the FTP areas or HTML storage areas. To give this access, you would go to each of the hierarchies that this group should have access to and see what groups they are assigned. Then, in /etc/group you need to do two things: First, create the webmaster group and place the users you need this access under that group. You can then add webmaster to the groups that already have access to the locations.

### Group Isolation

As a reverse of the other methods of using groups, you can also utilize groups to keep specific people out. Sometimes there are programs or files that most people on the system should have access to but perhaps interns or those who have not reached a certain security or trust clearance should not be able to see. A way to accomplish this is to create a group that holds the people that should not have access to those files—say, for example, "untrusted." Then, create a directory whose group ownership is that group. Set the permissions so that the owner and the world have access but the group itself does not. These permissions might look like rwx--rwx.

## Creating Shell Accounts

There are various tools available that allow you to create shell accounts quickly. In fact, there is one tool for each interface: a command line program, a GNU Network Object Model Environment (GNOME) tool, and a K Desktop Environment (KDE) tool.

### Creating Shell Accounts From The Command Line

Do the following to create a new shell account from the command line:

- 1. Log in as root.
- 2. Type “useradd *loginname*”. For example, to add the dog account, type “useradd dog”.

> *NOTE:* In Red Hat, you can use **adduser** instead of **useradd**. This is not true in all Linux distributions.

- 3. Before a user can log in, you have to assign a password. To do this, type “*passwd loginname*”.
- 4. At the prompt, enter the user’s initial password. This is a temporary password that you will give to the user, preferably over the phone. The user will be required to change it after the first login. Notice that you cannot see the password as you type. You can’t even see the number of letters you typed.
- 5. You are now prompted to retype the password to ensure there were no typos. Enter the password again. This entire password addition process might look like:

```
[root@den /root]# passwd dog
Changing password for user dog
New UNIX password:
Retype new UNIX password:
passwd: all authentication tokens updated successfully
```

### Creating Shell Accounts In GNOME

Do the following to create a new shell account within GNOME:

- 1. If GNOME is not already started, start it by typing either “startx” or “init 5” at the command line.
