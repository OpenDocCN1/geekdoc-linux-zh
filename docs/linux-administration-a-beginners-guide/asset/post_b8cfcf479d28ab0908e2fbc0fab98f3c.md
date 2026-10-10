
| Options | Descriptions |
|---|---|
| -g gid | Specifies the GID for the new group as gid. By default, this value is automatically chosen by finding the first available value. |
| -r | By default, Red Hat searches for the first GID that is higher than 499. The -r options tell groupadd that the group being added is a system group and should have the first available GID under 499. |
| -f | When adding a new group, Red Hat Linux will exit without an error if the specified group to add already exists. By using this option, the program will not change the group setting before exiting. This is useful in scripting cases where you want the script to continue if the group already exists. |
| group | This option is required. It specifies the name of the group you want to add to be group. |

### Table 5-2. More Command Options and Their Descriptions

### groupdel

Even more straightforward than userdel, the groupdel command removes existing groups specified in the /etc/group file. The only usage information needed for this command is this:

```
groupdel group
```

where group is the name of the group to remove. For example, if you wanted to remove the research group, you would issue this command:

```
[root@ford /root]# groupdel research
```

### groupmod

The groupmod command allows you to modify the parameters of an existing group. The options for this command are

```
groupmod -g gid -n group-name group
```

where the -g option allows you to change the GID of the group, the -n options allows you to specify a new name of a group, and of course you need to specify the name of the existing group as the last parameter.

For example, if the superman research group wanted to change its name to batman, you would issue the command:

```
[root@ford ~root]# groupmod -n batman superman
```

and you would be done.

### Using LinuxConf to Manipulate Users

The LinuxConf package is a remarkably powerful configuration tool that you will find yourself using for many different tasks. One of its features is its ability to create, delete, and modify user information.

To start LinuxConf, be sure you are logged in as the root user and have started the X Windows environment. If you are using GNOME with Enlightenment (Red Hat's default), you will see LinuxConf as a menu choice at the bottom left corner menu. If it doesn't appear there (or aren't using the default window manager), you can start LinuxConf by entering the command *linuxconf* from a terminal window.

Once you have started LinuxConf, you can scroll to the section on user management, which should look like Figure 5-1.

From this window, you can perform the three basic functions: add a new user, modify an existing user, and remove a user.

![](img/95b125a8bf06051f34d8aba73558b7eb_120_0.png)

Figure 5-1. Opening window to LinuxConf.

### Adding a User

To add a user, begin by clicking on the Add button at the bottom of the window. This will change the window as shown in Figure 5-2.

Every field except those in which the word (opt) (for optional) appears must be filled out. This includes the new account's login name and the user's real name. All other fields have default values associated with them. These parameters correlate to the entries in the useradd program.

Along with the basic user parameters, LinuxConf allows you to set some parameters regarding the user's permission to access some applications and e-mail settings if the user needs his e-mail forwarded to another address. These options are available via the window's tabs. Figure 5-3 shows the Privileges tab.

After you have established the parameters to your liking, click on the Accept button at the bottom of the window. The next window asks you to set the user's initial password. Once the password is set up, you are returned to the list of existing users, complete with your new addition.

![](img/95b125a8bf06051f34d8aba73558b7eb_121_0.png)

Figure 5-2. Adding a user with LinuxConf

![](img/95b125a8bf06051f34d8aba73558b7eb_122_0.png)

Figure 5-3. The Privileges tab when adding a user with LinuxConf.

### Modifying a User

Modifying a user's settings is quite simple. In LinuxConf's opening window, select the user whose settings you wish to modify. You'll see a window similar to that shown in Figure 5-4, which looks similar to the add user settings except it's completely filled out. All the fields in the window are modifiable. After all of the modifications are made, click Accept.

> **NOTE:** Remember that before you change a user's login or UID, make sure the user is not logged in or running any processes.

### Removing a User

To remove a user, click on the username from the user list as shown in Figure 5-1. Once you see the user's information, you should notice a button labeled Del at the bottom of the window. By clicking on this button, you begin the account removal process (Figure 5-5).

![](img/95b125a8bf06051f34d8aba73558b7eb_123_0.png)

Figure 5-4. Modifying a user with LinuxConf

![](img/95b125a8bf06051f34d8aba73558b7eb_123_1.png)

Figure 5-5. Removing a user with LinuxConf

Once you have decided what to do with the user’s home directory, click Accept to bring you back to the user list. If you chose to archive the user’s home directory, a gzipped tar file containing the data can be found in the /home/oldaccounts directory.

### Adding a Group

To add a new group, click Group Definitions on the left side of the LinuxConf opening window. This will bring up the list of current groups on the right of the window (Figure 5-6).

If you click the Add button, you’ll see a window in which you can fill in the name of a new group to be created. Although the window displays multiple fields, the only required field is the name of the group you want to create. All others have working defaults that the system will supply for you. After you’re finished, click Accept and you will be brought back to the list of groups, which should include the new group you added.

### Modifying a Group

Similar to modifying a user, to modify a group you simply select the name of the group you wish to edit from the group list to open a window similar to the add group window. This time the fields will be filled out with the group’s existing values. Simply change the fields you want and click Accept for the changes to take effect.

![](img/95b125a8bf06051f34d8aba73558b7eb_124_0.png)

Figure 5-6. Adding a group with LinuxConf

### Deleting a Group

To delete a group, select the group from the list of groups shown in Figure 5-6. You'll see the details of the group, below which will include a button labeled Del. Click Del to open a screen requiring you confirm your decision. Click Yes, and you'll see the list of groups, minus the group you just deleted.

## SETUID AND SETGID PROGRAMS

Normally, when a program is run by a user, it inherits all of the rights (or lack thereof) that the user has. If the user can't read the `/var/log/messages` file, neither can the program. Note that this permission can be different from the permissions of the user who owns the program file (usually called the binary). For example, the program `ls` (which is used to generate directory listings) is owned by the root user. Its permissions are set such that all users of the system can read the program. For example, if the user ssh runs `ls`, that instance of `ls` is bound to the permissions granted to the user ssh, not root.

However, there is an exception. Programs can be tagged with what's called a `SetUID` bit which allows a program to be run with permissions from the program's owner, not the user who is running it. Using `ls` as an example again, setting the `SetUID` bit on it and having the file owned by root means that if the user ssh runs `ls`, that instance of `ls` will run with root permissions, not with ssh's permissions. The `SetGID` bit works the same way, except instead of applying the file's owner, it is applied to the file's group setting.

To enable the `SetUID` bit or the `SetGID` bit, you need to use the `chmod` command, which is covered in detail in Chapter 6. To make a program `SetUID`, prefix whatever permission value you are about to assign it with a 4. To make a program `SetGID`, prefix whatever permission value you are about to assign it with a 2. For example, to make the `/bin/ls` a `SetUID` program (which is a bad idea, by the way), you would enter:

```
[root@ford /root]# chmod 4755 /bin/ls
```

## WHEN A FILE ISN'T OWNED

The title of this section is a bit misleading. A file is always owned, no matter what. A more accurate title would be: “When a File's Owner's UID Doesn't Map To an Entry in the `/etc/passwd` File” — but my editor was against that.

When a user is created, it gets a new and unique UID. Any files created by that user are owned by that user. To keep things easy, Linux doesn't use the user's name, but the UID, to file ownership. The system then uses the `/etc/passwd` file to perform a mapping between the user's UID and login so that an `ls` can make directory listings more human readable.

So what happens when a user is removed from the `/etc/passwd` file but files still exist that were owned by him? Nothing special, really. The most visible effect will be when you perform a directory listing on the file in question. Instead of showing you the owner
