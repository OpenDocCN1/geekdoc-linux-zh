
## TABLE 10-1 (continued)

| Option | Description |
| :--- | :--- |
| -p passwd | Enter a password for the account you are adding. This must be an encrypted password. Instead of adding an encrypted password here, you can simply use the passwd command later to add a password for the user. The user should be asked to immediately change the password you set. |
| -r | Allows you to create a new account with a user ID in the range reserved for system accounts. |
| -s shell | Specify the command shell to use for this account. Replace shell with the command shell. |
| -u user_id | Specify the user ID number for the account. The default behavior is to automatically assign the next available number. Replace user_id with the ID number. |

Next, set Robert's initial password using the passwd command. The passwd command prompts you to type the password twice. Asterisks are shown here to represent the password you type. Nothing is actually displayed when you type the password.

```
# passwd robert
Changing password for user robert.
New password: ******
Retype new password: ******
```

> **CROSS-REF** Refer to Chapter 13 for tips on picking good passwords.

In creating the account for Robert, the useradd command performs several actions:

- Reads the /etc/login.defs file to get default values to use when creating accounts.
- Checks command-line parameters to find out which default values to override.
- Creates a new user entry in the /etc/passwd and /etc/shadow files based on the default values and command-line parameters.
- Creates any new group entries in the /etc/group file.
- Creates a home directory based on the user's name and places it in the /home directory.
- Copies any files located within the /etc/skel directory to the new home directory. This usually includes login and application start-up scripts.

The preceding example uses only two of the available useradd options. Most account settings are assigned using default values. Here's an example that uses a few more options:

```
# useradd -m -g users -G wheel,sales -s /bin/tcsh -c "Connie James" connie
```

### Setting up and Maintaining User Accounts

In this case, the useradd command is told to create a home directory for the user connie (-m), make users the primary group she belongs to (-g), add her to the groups wheel and sales (-G), and assign tcsh as her primary command shell (-s). Note that the wheel and sales groups must already exist for this example to work. This results in a line similar to the following being added to the /etc/passwd file:

```
connie:x:502:100:Connie James:/home/connie:/bin/tcsh
```

In the /etc/passwd file, each line represents a single user account record. Each field is separated from the next by a colon (:) character. The field’s position in the sequence determines what it is. As you can see, the login name is first. The password field contains an x because CentOS is using a shadow password file in which to store encrypted password data. The user ID selected by the useradd command was 502. The primary group ID is 100, which corresponds to the users group in the /etc/group file. The comment field was correctly set to Connie James, the home directory was automatically assigned as /home/connie, and the command shell was assigned as /bin/tcsh, exactly as specified with the useradd options.

When you leave out many of the options (as I did in the first useradd example), default values are assigned in most cases. For example, by not using -g users or -G wheel,sales, a group named connie would have been created and assigned to the new user. Likewise, excluding -s /bin/tcsh causes /bin/bash to be assigned as the default shell.

The /etc/group file holds information about the different groups on your CentOS system and the users who belong to them. Groups are useful for allowing multiple people to share access to the same files while denying access to others. If you peek at the /etc/group file, you should find something similar to this.

```
bin:x:1:root,bin,daemon
daemon:x:2:root,bin,daemon
sys:x:3:root,bin,adm
adm:x:4:root,adm,daemon
tty:x:5:
disk:x:6:root
lp:x:7:daemon,lp
mem:x:8:
kmem:x:9:
wheel:x:10:root,robert,connie
nobody:x:99:
users:x:100:
timothy:x:500
robert:x:501
sales:x:601:robert,jessica,frankie
```

Each line in the group file contains the name of a group, the group ID number associated with it, and a list of users in that group. By default, each user is added to his or her own group, beginning with GID 500. Note that connie was added to the wheel and sales groups instead of having her own group.

## Part III Administration

It is actually rather significant that connie was added to the wheel group. By doing this, you grant her the ability to use the sudo command to run commands as the root user, provided that the wheel line is uncommented from the /etc/sudoers file, which it is not by default.

> Type `man sudo` in a Terminal window to learn more about the sudo command, and `man sudoers` to learn more about the sudoers file.

In this example, we used the -g option to assign connie to the users group. If you leave off the -g parameter, the default behavior is for useradd to create a new group with the same name and ID number as the user (assuming a group with the same ID does not already exist), which is assigned as the new user’s primary group. For example, look at the following useradd command:

```bash
$ useradd -m -G wheel,sales -s /bin/tcsh -c "Connie James" connie
```

It would result in an /etc/passwd line like this:

```text
connie:x:502:502:Connie James:/home/connie:/bin/tcsh
```

It would also result in a new group line like this:

```text
connie:x:502:
```

Note that the user ID and group ID fields now have the same number. If you set up all of your users this way, you will have a unique group for every user on the system, which allows for increased flexibility in the sharing of files among your users.

### Adding Users with User Manager

If you prefer a graphical window for adding, changing, and deleting user accounts, you can use the User Manager window. To open the window from the GNOME desktop, click on System > Administration > Users and Groups (or type system-config-users from a Terminal window as root). Figure 10-1 shows an example of it.

When you open the User Manager window, you see a list of all regular users who are currently added to your computer. Administrative users (UID 1–499) are not displayed. For each user, you can see the username, UID, primary group, full name, login shell, and home directory. Click any of those headings to sort the users by that information.

To add a new user from the User Manager window, do the following:

1. Click on the Add User icon to open the Create New User window (see Figure 10-2).
2. Type the requested information in the following fields:
   - “User Name”—A single word to describe the user. Typically, the username is eight characters, all lowercase, containing the user’s real first name, last name, or more often a combination of the two.

#### FIGURE 10-1

Manage users from the User Manager window.

![](img/2f265415ceec72538dd3c78ffca75c10_434_0.png)

#### FIGURE 10-2

The Create New User window

![](img/2f265415ceec72538dd3c78ffca75c10_434_1.png)

   - “Full Name” — The user's full name. This name is typically just used for display, so using uppercase and lowercase is fine.
   - “Password” — The user's initial password. Ask the user to change this password the first time he or she logs in to the new account, which the user can do by running the `passwd` command.
   - “Confirm Password” — Type the password again, to make sure you entered it correctly.
   - “Login Shell” — The default shell that the user sees when first logging in to CentOS from a character display
   - “Create home directory” — By default, this box is selected and the user’s home directory is created automatically.
   - “Home Directory” — By default, the user is given a home directory of the user’s name in the /home directory. For example, the user jessica would be assigned /home/jessica as her home directory. Change this field if you want to assign the user to a different home directory.
   - “Create a private group for the user” — Check this box if you want a group by the same name as the user, created for this user. The name is added to the /etc/group file. This feature is referred to as user private groups (UPGs).¹
   - “Specify user ID manually” — Typically, you would not check this box, so that the UID for the new user would be assigned automatically. New UIDs for regular users start at 500. However, if you want to assign a particular UID for a user (e.g., if you want to match the UID with the user’s UID from another computer on your network), select this box and type the number you want to use in the UID box.
3. Click OK when you are done. The new user is added to the /etc/passwd and /etc/group files. The user account is now available for use to log in.

> **NOTE** Using user private groups (UPGs) can be a benefit for sharing a directory of files among several users. Here’s an example:

```
# useradd -m projectx
# mkdir /usr/local/x
# chown root.projectx /usr/local/x
# chmod 2775 /usr/local/x
# ls -ld /usr/local/x
drwxrwx-x 2 root projectx 4096 May 12 04:31 /usr/local/x
# gpasswd -a nextuser projectx
```

In this example, you create a user named projectx (with a group named projectx). Create a /usr/local/x directory and have it owned by root user and projectx group. Set the setgid bit to be on for the group (2), open full Read/Write/Execute permissions for user and group (77), and open Read and Execute permissions for everyone else (5). Add each user to the group (add) that you want to be able to write to the projectx directory (replace nextuser with the user you want to add). After that, regardless of a user’s primary group, any file created in the /usr/local/x directory by a user can be read or modified by anyone in the projectx group.

### Setting User Defaults

The useradd command and User Manager window both determine the default values for new accounts by reading the /etc/login.defs file. You can modify those defaults by either editing that
