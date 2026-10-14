
> **NOTE**
>
> All fields in the `+` entry may be overridden except for the user ID.
>
> An entry of the form `-name` means that the group is disallowed. All subsequent entries for that group name, whether in the NIS group file or in the local `/etc/group` file, are ignored.

> **CAUTION**
>
> As is the case with `/etc/passwd`, the `/etc/group` file must not contain any blank lines. Blank lines can cause unpredictable behavior in system administration software that uses the file.
>
> For more information on `/etc/group`, use the `man 5 group` command.

## User Account and Group Management Applications

There are two basic types of applications you can use when managing user accounts and groups on SUSE systems:

- The graphical system assistant application, YaST
- A suite of command-line tools

> **NOTE**
>
> For more information about YaST, refer to Chapter 2, “Updating the Server.”

While both YaST and the command-line utilities perform essentially the same task, the command-line tools have the advantage of being scriptable and, therefore, more easily automated. On the other hand, YaST provides a wizard-like graphical interface that walks you through the necessary steps.

Table 4.3 describes some of the more common command-line tools used to create and manage users.

**TABLE 4.3**
**User Management Command-Line Tools**

| APPLICATION | FUNCTION |
|---|---|
| `/usr/sbin/useradd` | Creates a user account using default values from `/etc/default/useradd`. This tool is also used to specify a user's primary and secondary group memberships. |
| `/usr/sbin/userdel` | Deletes user accounts. |
| `/usr/sbin/usermod` | Updates account attributes including some functions related to password aging, as well as primary and secondary group membership. For more fine-grained control, use the `passwd` command. `usermod` can be used to make changes to LDAP users with the help of the `-D` and `-L` LDAP options. |
| `/usr/bin/passwd` | Sets passwords. Although primarily used to change a user's password, it also controls all aspects of password aging. It is really the “Swiss-army knife” password utility. |
| `/usr/sbin/chpasswd` | Batch changes user passwords by reading in a file consisting of username and password pairs. |
| `/usr/bin/chage` | Changes the user's password-aging policies. The `passwd` utility can also be used for this purpose. |
| `/usr/bin/chfn` | Changes the user's GECOS information. Can also use `passwd -f` instead. |
| `/usr/bin/chsh` | Changes the user's default shell. Can also use `passwd -s` instead. |
| `/usr/sbin/pwck` | Checks the integrity of the `/etc/passwd` and `/etc/shadow` files. |

Table 4.4 lists some of the more common command-line tools used to create and manage groups.

**TABLE 4.4**
**Group Management Command-Line Tools**

| APPLICATION | FUNCTION |
|---|---|
| `/usr/sbin/groupadd` | Creates new groups, but does not assign users to those groups. The `useradd` and `usermod` programs should then be used to assign users to and remove them from a given group. |
| `/usr/sbin/groupdel` | Deletes groups. |
| `/usr/sbin/groupmod` | Modifies group names or GIDs, but does not change group membership. The useradd and usermod programs should be used to assign users and to remove them from a given group. |
| `/usr/bin/gpasswd` | Changes group passwords (stored in `/etc/group`) to allow nongroup members who know the group password to join the group. Only root may change group passwords. (You can also use `gpasswd -g` to change the group password.) |
| `/usr/sbin/grpck` | Checks the integrity of the `/etc/group` file. (On older versions of SUSE Linux, such as SLES 8, grpck also checks the `/etc/gshadow` file; SLES 9 and later no longer use a group shadow file.) |

To learn more about the utilities in Table 4.4, refer to the man page for each (for example, `man grpck`).

> **NOTE**
>
> The applications listed in Tables 4.3 and 4.4 do not determine what resources these users and groups have control over. For this, you must use applications that deal with file permissions, some of which are discussed in Chapter 6, “Filesystem Security.”

## Creating and Editing User Accounts

When you need to create or modify a single user account or a small number of accounts (say, fewer than five), it is usually more convenient to use YaST for the task because of its GUI interface. Otherwise, you may want to consider creating some shell scripts for the task using command-line tools discussed later in this section.

> **TIP**
>
> Many user-creation scripts are available on the Internet. A sample skeleton bash script for creating new users (using the useradd command) can be found at http://www.osix.net/modules/article/?id=577.

Use the following steps to create a new user account using YaST:

1. Launch YaST using one of the following methods:
   - From the KDE desktop, click on the YaST icon. Enter the root password if prompted.
   - From the KDE desktop, select Applications, System, YaST. Enter the root password if prompted.
   - From a terminal window, first run `sux` to become root (if not root already) and then run `yast2` (the GUI version).
   - From a terminal window, first run `su` to become root (if not root already) and then run `yast` (the ncurses version).

2. From the YaST Control Center, select Security and Users, Edit and Create Users to launch the User and Group Administration module. (If the NIS, LDAP, Samba, or Kerberos authentication is configured, you will be prompted for additional passwords.)

> **TIP**
>
> You can run `yast` and `yast2` with the parameter `users` (for example, `yast users`) so YaST automatically launches the User and Group Administration module instead of displaying the Control Center menu.

3. From the User and Group Administration screen (see Figure 4.1), select Set Filter and choose the type of user accounts (such as Local Users, System Users, or LDAP Users) you want to manage. A list of current users of the selected type is displayed. You may only see Local Users and System Users available as selections under the Set Filter drop-down list. Additional selections (such as LDAP Users) will be available only after you have configured and started the services on the server.

> **TIP**
>
> You can combine multiple user types (such as Local Users and LDAP Users) to be displayed under the Custom filter by editing the selections in Set Filter, Customize Filter, Custom view.

4. Select the Add option, and a screen similar to Figure 4.2 is displayed.

## FIGURE 4.1
The User and Group Administration module screen in YaST.

![](img/ae8469257d2662b469f2360b3bbbe322_118_0.png)

## FIGURE 4.2
Adding a new local user.

![](img/ae8469257d2662b469f2360b3bbbe322_118_1.png)

5. Fill in the user’s name, login ID, and password. Keep in mind that both login names and passwords are case sensitive. Valid passwords can be composed of any of the (7-bit) ASCII characters, including digits and upper- and lowercase letters. However, you should use only printable ASCII characters whose decimal values are between the range of 33 and 126. Spaces (dec. 32) do work if you have a pure Linux/Unix environment but may fail with connections from an X emulator or SSH client from a Windows client. Therefore, you should avoid spaces in passwords. Furthermore, depending on the encryption algorithm (such as DES, which is the default), you may be limited to use only up to eight alphanumeric characters. (See “Use a Strong Password-Hashing Algorithm” later in this chapter.)

6. Click Password Settings if you want to change the settings (such as password expiration date) for the new user to something other than the defaults. In many cases, the default settings are sufficient and don’t need to be modified.

7. Click Details if you want to change settings such as UID, home directory location, default login shell, and group memberships; the Additional User Information field in this screen corresponds to the GECOS field in /etc/passwd. (Remember that if you plan to run the finger daemon, the information in this field must be in the particular form required by finger; see the earlier “What Is the GECOS Field?” sidebar.) The UIDs are assigned automatically, based on the previously used value, and default settings are read from /etc/default/useradd.

> **TIP**
>
> The shells shown in the drop-down list of the Login shell are read from the /etc/shells file. Edit this file to remove any entry that you don’t want to show up. Keep in mind that having an entry in /etc/shells does not necessarily mean the actual shell exists on the server. You should check to ensure the program exists before you include it in the list. This file is also referenced by csh.
>
> You may notice an entry called /bin/bash1 in /etc/shells, but it is not listed in the drop-down list. /bin/bash1 is an old reference to version 1 of bash, and /bin/bash is a general reference to the current version of bash, which is version 2. YaST filters out /bin/bash1 using the /usr/share/YaST2/modules/Users.pm Perl script.

8. Click Create when you are satisfied with the user’s settings.

9. Repeat steps 4 through 8 to create more users. Click Finish when you are done. You must click Finish for the databases to be updated. Otherwise,
