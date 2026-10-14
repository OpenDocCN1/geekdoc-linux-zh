
The entry contains seven data fields, each separated by a colon:

- The username
- A placeholder for the password
- The user ID number
- The group ID number
- The full name of user
- The home folder of the user
- The default shell

In the original days of Linux, the /etc/passwd file contained the actual encrypted version of the user’s password. However, the /etc/passwd file must be readable to all users on the system so that the system can validate them. This requirement left the user passwords vulnerable to brute-force attacks using password-cracking software.

The solution to the problem was to hide the actual passwords in a separate file that’s not readable by any user.

## The /etc/shadow File

The /etc/shadow file is a secure file where Ubuntu stores the actual user account password, along with some other information about the account. Just like the /etc/passwd file, the /etc/shadow file contains a separate line for each user account.

A sample line from the /etc/shadow file looks like this:

```
rblum:Ep6gekHkChF.:10063:0:99999:7:::
```

The shadow password file contains eight data fields, each separated by a colon:

- The username
- The encrypted password
- The number of days since the password was last changed
- The number of days before the password may be changed
- The number of days after which the password must be changed
- The number of days to warn the user of an upcoming password change
- The number of days since January 1, 1970, that the account has been disabled
- Reserved data field that’s not used

## The Groups File

Ubuntu keeps track of all the group information in the /etc/group file. This file has each group on a separate line, using the format:

```
admin:x:115:rich
```

The group file contains four data fields, each separated by a colon:

- The group name
- A password, if assigned to the group
- The group ID value
- A comma-separated list of user accounts that belong to the group

## Part 3: Managing Your Workstation

![](img/39e65eeb4f54001ede08c6114ae3cc6c_449_0.png)

> Because Ubuntu doesn’t use a specific root user account to administer the system, keeping at least one user account in the admin group is a must. If you accidentally remove all of the users from the admin group, no one will be able to add software patches or updates, add new users, or even move users to other groups.
> 
> If this happens to you, don’t worry, there’s a solution. Just follow these steps to get things back to normal:
> 
> 1. Boot your workstation using the Ubuntu LiveCD.
> 2. Mount the workstation hard drive on the LiveCD’s virtual file system.
> 3. Open a Terminal session on the LiveCD.
> 4. Use the command-line navigation commands (discussed in Chapter 19, “The Ubuntu Command Line”) to navigate to the mount point of the workstation hard drive, then to the `/etc` folder on the hard drive.
> 5. Use a text editor to open the group file.
> 6. Find the admin group and add a username from your system onto the line. To append a value to a line in the vi editor, use the `A` command.
> 7. Exit and save the file.
> 8. Reboot the workstation and let the normal Ubuntu installation on the hard drive boot.
> 
> Once you’ve added the username to the admin group, it should have administrator privileges on the workstation.

## Using the Command Line

Although it can be done, it's usually not a good idea to directly edit the `/etc/passwd` or `/etc/group` files. Bad things can happen, and you wouldn’t want them to happen while you’re in the middle of editing one of those two files!

Instead, the safer way to manage user and group accounts from the command line is to use the two commands explained in this section.

## The User Commands

When working on the command line, you should use the `adduser` command to create a new user or add a user to an existing group. To add a user with the `adduser` command, use this format:

```
sudo adduser --home /home/rich rich
```

This command creates the new user account, `rich`, and creates a home folder at `/home/rich` for the account.

You can also use the `adduser` command to add an existing user account to a group:

```
sudo adduser rich users
```

This command adds the username `rich` to the `users` group.

The `deluser` command deletes a user account from the system:

```
sudo deluser rich
```
