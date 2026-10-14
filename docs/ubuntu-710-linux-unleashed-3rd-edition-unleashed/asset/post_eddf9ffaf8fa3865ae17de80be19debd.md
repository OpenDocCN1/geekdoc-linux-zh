
his special shell, and the -u option to specify her UID. (If we create a user with the default settings, we do not need to use these options.) All we want to do can be accomplished on one line:

```
$ sudo useradd bernice -p Sticher -s /bin/zsh -u 1002
```

The sysadmin can also use the graphical interface that Ubuntu provides, as shown in Figure 10.2. It is accessed as the Users and Groups item from the Administration menu. Here, the sysadmin is adding a new user to the system where user bernice uses the bash command shell.

These are the steps we used to add the same account as shown in the preceding command, but using the graphical User Manager interface:

- 1. Launch the Ubuntu User Manager graphical interface by clicking on the Users and Groups menu item found in the System Settings menu.
- 2. Click the Add User button to bring up the Add User dialog window.
- 3. Fill in the form with the appropriate information as requested, ensuring you create a good password.
- 4. Click the Advanced tab and open the drop-down Shell menu to select the bash shell.
- 5. Using the arrows found in the UID dialog, increment the UID to 1413.
- 6. Click OK to save the settings.

Note that the user is being manually assigned the UID of 1413 because that is her UID on another system machine that will be connected to this machine. Because the system only knows her as 1001 and not as bernice, the two machines would not recognize bernice as the same user if two different UIDs were assigned.

> **NOTE**
> 
> A Linux username can be any alphanumeric combination that does not begin with a special character reserved for shell script use (see Chapter 11 for disallowed characters, mostly punctuation characters). In Chapter 4, we told you that usernames are typically the user’s first name plus the first initial of her last name. That is a common practice on larger systems with many users because it makes life simpler for the sysadmin, but is neither a rule nor a requirement.

## Monitoring User Activity on the System

Monitoring user activity is part of the sysadmin’s duties and an essential task in tracking how system resources are being used. The w command tells the sysadmin who is logged in, where he is logged in, and what he is doing. No one can hide from the super user. The w command can be followed by a specific user’s name to show only that user.

![](img/7aaa8e4f2209bf9f2fb443905096e94c_233_0.png)

FIGURE 10.2 Adding a new user is simple. The GUI provides a more complete set of commands for user management than for group management.

The ac command provides information about the total connect time of a user measured in hours. It accesses the /var/log/wtmp file for the source of its information. The ac command proves most useful in shell scripts to generate reports on operating system usage for management review. Note that to use the ac command, you will have to install the acct package using either synaptic or apt-get.

> TIP
> 
> Interestingly, a phenomenon known as timewarp can occur in which an entry in the wtmp files jumps back into the past and ac shows unusual amounts of time accounted for users. Although this can be attributed to some innocuous factors having to do with the system clock, it is worthy of investigation by the sysadmin because it can also be the result of a security breach.

The last command searches through the /var/log/wtmp file and lists all the users logged in and out since that file was first created. The user reboot exists so that you might know who has logged in since the last reboot. A companion to last is the command lastb, which shows all failed, or bad, logins. It is useful for determining whether a legitimate user is having trouble or a hacker is attempting access.

## NOTE

The accounting system on your computer keeps track of usage user statistics and is kept in the current /var/log/wtmp file. That file is managed by the init and login processes. If you want to explore the depths of the accounting system, use the GNU info system: info accounting.

## Managing Passwords

Passwords are an integral part of Linux security, and they are the most visible part to the user. In this section, you learn how to establish a minimal password policy for your system, where the passwords are stored, and how to manage passwords for your users.

### System Password Policy

An effective password policy is a fundamental part of a good system administration plan. The policy should cover the following:

- ► Allowed and forbidden passwords
- ► Frequency of mandated password changes
- ► Retrieval or replacement of lost or forgotten passwords
- ► Password handling by users

### The Password File

The password file is /etc/passwd, and it is the database file for all users on the system. The format of each line is as follows:

```
username:password:uid:gid:gecos:homedir:shell
```

The fields are self-explanatory except for the gecos field. This field is for miscellaneous information about the user, such as the users' full name, his office location, office and home phone numbers, and possibly a brief text message. For security and privacy reasons, this field is little used nowadays, but the system administrator should be aware of its existence because the gecos field is used by traditional UNIX programs such as finger and mail. For that reason, it is commonly referred to as the finger information field. The data in this field will be comma delimited; the gecos field can be changed with the chfn (change finger) command.

Note that a colon separates all fields in the /etc/passwd file. If no information is available for a field, that field is empty, but all the colons remain.

If an asterisk appears in the password field, that user will not be permitted to log on. Why does this feature exist? So that a user can be easily disabled and (possibly) reinstated later without having to be created all over again. The system administrator manually edits this field, which is the traditional UNIX way of accomplishing this task. Ubuntu provides improved functionality with the passwd -l command mentioned earlier.
