
The following is a sample `/etc/passwd` file:

```
```text
at:x:25:25:Batch jobs daemon:/var/spool/atjobs:/bin/bash
bin:x:1:1:bin:/bin:/bin/bash
daemon:x:2:2:Daemon:/sbin:/bin/bash
ftp:x:40:49:FTP account:/srv/ftp:/bin/bash
games:x:12:100:Games account:/var/games:/bin/bash
gdm:x:50:15:Gnome Display Manager daemon:/var/lib/gdm:/bin/bash
haldaemon:x:101:102:User for haldaemon:/var/run/hal:/bin/false
lp:x:4:7:Printing daemon:/var/spool/lpd:/bin/bash
...
geeko:x:1000:100:Geeko Chameleon:/home/geeko:/bin/bash
```
```

Each line in the `/etc/passwd` file represents one user and contains the information shown in Figure 9-9 (separated by colons).

![](img/9129877170834ca9d5fdac5319bf5f12_297_0.png)

Note the following about the fields in each line:

- *User-name*—This is the name a user enters to log in to the system (login name).
- *Password*—The x in this field means that the password is stored in the `/etc/shadow` file.
- *UID*—In compliance with the Linux standards, three number ranges are reserved:
  - 0 for root
  - 1–99 for the system itself
  - 100–499 for special system users (such as services and programs)
  - 1000+ for normal users
- *GID*—Number of the group. In compliance with the Linux standards, two number ranges are reserved:
  - 0–99 for special system groups, including root (such as services and programs)
  - 100+ for normal groups
- *Comments field*—Normally, the full name of the user is stored here. Information such as a room number or telephone number can also be stored here.

- *Home directory*—The personal directory of a user is normally in the /home directory and has the same name as the user (login) name.
- *Login shell*—This is the shell that is started for a user after he or she has successfully logged in. In Linux, this is normally /bin/bash (Bourne Again shell). The shell must be listed in the /etc/shells file.

![](img/9129877170834ca9d5fdac5319bf5f12_298_0.png)

For additional information on this file, enter man 5 passwd.

The shell must be listed in the /etc/shells file.

## /etc/shadow

The /etc/shadow file stores encrypted user passwords and password expiration information. Most Linux systems use shadow passwords.
The file can only be changed by the user root and read by the user root and members of the group shadow. The following is a sample /etc/shadow file:

```
at:!:13181:0:99999:7:::
bin:*:13181::::::
daemon:*:13181::::::
ftp:*:13181::::::
games:*:13181::::::
gdm:!:13181:0:99999:7:::
lp:*:13181::::::
root:$2a$05$QMXZcvOmOHNErjGvCGHOPW5Kp9faXxRE4Bsg3B4DIRLtPGpU1Ba:13181:0:99999:7:-1::
xay0u3:$2a$05$QMXZcvOmOHNErjGvCGHOPW5Kp9faXxRE4Bsg3B4DIRLtPGpU1Ba:13181::::::
sshd:!:13181:0:99999:7:::
ucp:*:13181::::::
wwwrun:+:13181::::::
geeko:$2a$05$QMXZcvOmOHNErjGvCGHOPW5Kp9faXxRE4Bsg3B4DIRLtPGpU1Ba:13181:0:99999:7:-1::
```

Each line in the /etc/shadow file belongs to one user and contains the fields shown in Figure 9-10.

![](img/9129877170834ca9d5fdac5319bf5f12_298_1.png)

Figure 9-10

Figure 9-10 shows the entry for the user geeko with an encrypted password. The plain text password is novel1.

The encrypted password is coded with the Blowfish algorithm. The encrypted word consists of letters, digits, and some special characters. If an invalid character (such as “*” or “!”) occurs in the Password field, that user has an invalid password.

Many users, such as wwwrun (Apache Web server) or bin have an asterisk (“*”) in the Password field. This means that these users cannot log in to the system, but are needed for special applications.

If the Password field is empty, then the user can log in to the system without entering a password. A password should always be set in a Linux system.

The information at the end of each line determines some limits:

- *Last Change*—Date of last password change. The number represents the number of days since January 1, 1970.
- *Next Possible Change*—Minimum age of a password before a user can change it.
- *Next Obligatory Change*—Number of days a user can use the same password before it expires.
- *Warning*—Number of days users get a warning before password expiration. Enter −1 to disable the warning.
- *Limit*—Number of days after the password expires that the user can continue to log in. Enter −1 for unlimited access. (This does not make sense, of course.)
- *Lock*—Date when the account expires. The date must be in the format YYYY-MM-DD. Leave the field empty if the account never expires.

## /etc/group

The /etc/group file stores group information. The following is a sample /etc/group file.

```
at:!:25:
audio:x:17:
bin:x:1:daemon
cdrom:x:20:
console:x:21:
...
video:x:33:geeko
wheel:x:10:
www:x:8:
xok:x:41:
users:x:100:
```

Each line in the file represents a single group record, and contains the group name, the GID (Group ID), and the members of the group. For example, this is the entry for the group video in the /etc/group file:

```
video:x:33:geeko
```

The first field identifies the group (video). The second field (x) is the Password field. The third field displays the GID (33), and the fourth field identifies geeko as a member of the group video. The /etc/group file shows secondary group memberships, but it does not identify the primary group for a user.

![](img/9129877170834ca9d5fdac5319bf5f12_300_0.png)

## Exercise 9-1: Manage User Accounts with YaST and Get User and Group Information from the Command Line

In this exercise, first create and remove a user account with the YaST User Management module. Perform the following tasks:

- Create a new account labeled `tux` for the user Tux Penguin with the password of `novell`.
- Log in as the new user `tux`.
- Open the `/etc/passwd` file and look for the entries for `geeko` and `tux`.
- Log in as `geeko` and remove `tux`’s account using YaST.

Then, get information on some users and groups from the command line. Perform the following tasks:

- Find out the GIDs of the `ftp`, `lp`, `nobody`, `root`, `www`, and `users` groups (stored in `/etc/groups`).
- Find out the UIDs of the `ftp`, `lp`, `nobody`, `root`, `wwwrun`, and `geeko` users (stored in `/etc/passwd`).
- Compare the identity info of the `root` and `geeko` users (use the `id` command).

![](img/9129877170834ca9d5fdac5319bf5f12_300_1.png)

## Detailed Steps to Complete This Exercise

- Part I: Create a New User Account with YaST
- Part II: Log In as the New User
- Part III: View the passwd File
- Part IV: Log In as User geeko and Remove the New User Account
- Part V: Get User and Group Information from the Command Line

### Part I: Create a New User Account with YaST

To create a new user account with YaST, do the following:

- 1. Start YaST by doing the following:
  - a. From the GNOME desktop, select Computer > More Applications > System > YaST.
  - b. In the Password Needed dialog, type a password of `n0v3ll`.
  - c. Select Continue.
  The YaST Control Center appears.
- 2. From the YaST Control Center, select Security and Users > User Management.
- 3. Add a new user by selecting **Add**.
- 4. Enter the following information:
  - *User’s Full Name*—Tux Penguin
  - *Username*—tux
  - *Password*—novell
  - *Confirm Password*—novell
- 5. When you finish, select **Accept**.
- 6. Confirm the password warning by selecting **Yes**.
- 7. Repeat Steps 3 to 6 to create another user with the following information:
  - *User’s Full Name*—Mary Novell
  - *Username*—mary
  - *Password*—novell
  - *Confirm Password*—novell
- 8. Save the new settings by selecting **Finish**.
- 9. Close the YaST window.

### Part II: Log In as the New User

To log in as the new user, do the following:

- 1. From the bottom panel, log out by selecting **Computer > Logout**.
- 2. In the Logout dialog, select **Log Out**.
  X Window is restarted and the GUI login screen appears.
- 3. In the Username field, enter `tux`; then press **Enter**.
- 4. In the Password field, enter `novell`; then press **Enter**.
- 5. Close or cancel any displayed dialogs.

### Part III: View the passwd File

To view the passwd file, do the following:

- 1. Start the Nautilus file manager by double-clicking tux’s Home icon on the desktop.
  The content of tux’s home directory is displayed.
- 2. Browse to the /home directory.
  Notice there are two directories for users tux and geeko.
- 3. Browse to the /etc directory.
- 4. Open the passwd file by double-clicking on it.
  Notice the entries for users tux and geeko at the end of the file.
- 5. Close all windows.
