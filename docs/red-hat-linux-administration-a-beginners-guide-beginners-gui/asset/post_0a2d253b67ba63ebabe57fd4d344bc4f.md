
## Progress Check

- 1. Name the fields stored in the /etc/passwd file.
- 2. Name the fields stored in the /etc/shadow file.
- 3. Name the fields stored in the /etc/group file.

## CRITICAL SKILL 5.3
Employing User Management Tools

The wonderful part about having password database files that have a well-defined format in straight text is that it is easy for anyone to be able to write his or her own management tools. Indeed, many site administrators have already done this in order to integrate their tools along with the rest of their organization’s infrastructure. They can start a new user from the same form that lets them update the corporate phone and e-mail directory, LDAP servers, web pages, and so on. Of course, not everyone wants to roll their own tools, which is why Linux comes with several prewritten tools that do the job for you.

In this section, you’ll learn about user management tools that work from both the command-line interface and the graphical user interface (GUI). Of course, learning how to use both is the preferred route, for you never know under what circumstances you may one day find yourself adding users.

## Command-Line User Management

You can choose from among six command-line tools to perform the same actions performed by the GUI tool: useradd, userdel, usermod, groupadd, groupdel, and groupmod. The obvious advantage to using the GUI tool is ease of use. However, the disadvantage is that actions that can be performed with it cannot be automated. This is where the command-line tools become very handy.

- 1. The /etc/passwd file contains the following colon-delimited fields: login name; encrypted password; UID; default GID; full user name; home directory; and login shell.
- 2. The /etc/shadow file contains the following colon-delimited fields: login name; encrypted password; days since Jan. 1, 1970, that the password was changed; days before the password may be changed; days after which the password must be changed; days before the password is about to expire that the user is warned; days after the password is expired that the account is disabled; days since Jan. 1, 1970, that the account has been disabled; and a reserved field.
- 3. The /etc/group file contains the following colon-delimited fields: group name; encrypted password for the group; GID number; and a comma-separated list of member users.

![](img/ec2066d370d3af1a767664d36aa7ddfe_147_0.png)

Linux distributions other than Red Hat may have slightly different parameters than the tools used here. To see how your particular installation is different, read the man page for the particular program in question.

## useradd

As the name implies, **useradd** allows you to add a single user to the system. Unlike the GUI tool, it offers no interactive prompts. Instead, all parameters must be specified on the command line. Here’s how you use this tool:

```
useradd [-c comment] [-d homedir] [-e expire date] [-f inactive time] [-g initial group][-G group[,…]] [-m [-k skelton dir]] [-M] [-s shell] [-u uid [-o]] [-n] [-r] login
```

Don’t be intimidated by this long list of options! You’ll examine them one at a time and discuss their relevance.

Before you dive into these options, take note that anything in the square brackets is optional. Thus, to add a new user with the login **rwhite**, you could issue a command as simple as this:

```
[root@tedford /root]# useradd rwhite
```

Default values are used for any unspecified values. (To see the default values, simply run **useradd -D**; the module will describe how to change the defaults shortly.) Table 5-1 shows the command options and their descriptions.

| Option | Description |
|:-------|:------------|
| -c comment | Allows you to set the user’s name in the GECOS field. As with any command-line parameter, if the value includes a space, you will need to put quotes around the text. For example, to set the user’s name to Russell White, you would have to specify -c “Russell White”. |
| -d homedir | By default, the user’s home directory is /home/login (for example, if the login is rwhite, the home directory would be /home/rwhite). When creating a new user, the user’s home directory gets created along with the user account. So if you want to change the default to another place, you can specify the new location with this parameter—for example, -d /home/sysadmin/rwhite. |
| -e expire-date | It is possible for an account to expire after a certain date. By default, accounts never expire. To specify a date, be sure to place it in MM/DD/YY format (specify 00 for the year 2000 for this system)—for example, use -e 04/01/03 for the account to expire on April 1, 2003. |

**Table 5-1** Options for the useradd Command

| Option | Description |
| :--- | :--- |
| -f inactive-time | This option specifies the number of days after a password expires that the account is still usable. A value of `-1` (zero) indicates that the account is disabled immediately. A value of `0` will never allow the account to be disabled, even if the password has expired (for example, `-f 3` will allow an account to exist for three days after a password has expired). The default value is `-1`. |
| -g initial-group | Using this option, you can specify the default group the user has in the password file. You can use a number or name of the group; however, if you use a name of a group, the group must exist in the `/etc/group` file—for example, `-g project`. |
| -G group[,...] | This option allows you to specify additional groups to which the new user will belong. If you use the `-G` option, you must specify at least one additional group. You can, however, specify additional groups by separating them with commas. For example, to add a user to the project and admin groups, you should specify `-G project,admin`. |
| -m [-k skel-dir] | By default, the system automatically creates the user’s home directory. This option is the explicit command to create the user’s home directory. Part of creating the directory is copying default configuration files into it. These files come from the `/etc/skel` directory by default. You can change this by using the secondary option `-k skel dir`. (You must specify `-m` in order to use `-k`.) For example, to specify the `/etc/admiskel` directory, you would use `-m -k /etc/admiskel`. |
| -M | If you used the `-m` option, you cannot use `-M`, and vice versa. This option tells the command not to create the user’s home directory. |
| -n | Red Hat Linux creates a new group with the same name as the new user’s login as part of the process of adding a user. You can disable this behavior by using this option. |
| -s shell | A user’s login shell is the first program that runs when a user logs in to a system. This is usually a command-line environment, unless you are logging in from the X login screen. By default, this is the Bourne Shell (`/bin/bash`), though some folks like other shells such as the Turbo C Shell (`/bin/tcsh`). This option lets you choose whichever shell you would like to run for the new user upon login. (A list of shells is available in `/etc/shells`.) |
| -u uid | By default, the program will automatically find the next available UID and use it. If for some reason you need to force a new user’s UID to be a particular value, you can use this option. Remember that UIDs must be unique for all users. |
| login | Finally, the only parameter that **isn’t optional**! You must specify the new user’s login name. |

Table 5-1 Options for the useradd Command (*continued*)

For example, to create a new user whose name is Mike Pawlawski, who is a member of the admin and support groups (default group admin), and who prefers using the Turbo C Shell and wants the login name `mpawlawski`, you would use this line:

```
[root@tedford /root]# useradd -c "Mike Pawlawski" -g admin -G support \
> -s /bin/tcsh mpawlawski
```

## userdel

The **userdel** command does the exact opposite of **useradd**—it removes existing users. This straightforward command has only one optional parameter and one required parameter:

```
userdel [-r] username
```

By running the command with only the user's login specified on the command line, for example, **userdel rwhite**, all of the entries in the `/etc/passwd` and `/etc/shadow` files, and references in the `/etc/group` file, are automatically removed. By using the optional parameter (for example, **userdel -r rwhite**) all of the files owned by the user in his home directory are removed as well.

## usermod

The **usermod** command allows you to modify an existing user in the system. It works in much the same way as **useradd**. The exact command-line usage is as follows:

```
usermod [-c comment] [-d homedir] [-m] [-e expire date]
[-f inactive time] [-g initial group]
[-G group[,...]] [-l login] [-s shell]
[-u uid] login
```

Every option you specify when using this command results in that particular parameter being changed about the user. All but one of the parameters listed here are identical to the parameters documented for the **useradd** program. That one option is -l.

The -l option allows you to change the user's login name. This and the -u option are the only options that require special care. Before changing the user's login or UID, you must make sure the user is not logged in to the system or running any processes. Changing this information if the user is logged in or running processes will cause unpredictable results.

Here's an example of using **usermod** to change user **mpawlowski** such that his comment field reads Number Nine instead of Mike Pawlowski:

```
[root@tedford /root]# usermod -c "Number Nine" mpawlowski
```

## groupadd

The group commands are similar to the user commands; however, instead of working on individual users, they work on groups listed in the `/etc/group` file. Note that changing group information does not cause user information to be automatically changed. For example, if you remove a group whose GID is 100 and a user's default group is specified as 100, the user's default group would not be updated to reflect the fact that the group no longer exists.

The **groupadd** command adds groups to the `/etc/group` file. The command-line options for this program are as follows:

```
groupadd [-g gid] [-r] [-f] group
```

Table 5-2 shows command options and their descriptions.
