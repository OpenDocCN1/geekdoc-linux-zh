operating system. The most typical way to add a user is with the adduser command, which takes a required argument: the username for the new user that you would like to create.

The adduser command asks a few questions before creating the account but its usage is fairly straightforward. Its configuration file, /etc/adduser.conf, includes many interesting settings. You can, for example, define the range of user identifiers (UIDs) that can be used, dictate whether or not users share a common group or not, define default shells, and more.

The creation of an account triggers the population of the user's home directory with the contents of the /etc/skel/ template. This provides the user with a set of standard directories and configuration files.

In some cases, it will be useful to add a user to a group (other than their default main group) in order to grant additional permissions. For example, a user who is included in the sudo group has full administrative privileges through the sudo command. This can be achieved with a command such as adduser user group.

> **Using getent to Consult the User Database**
> The getent (get entries) command checks the system databases (including those of users and groups) using the appropriate library functions, which in turn call the name service switch (NSS) modules configured in the /etc/nsswitch.conf file. The command takes one or two arguments: the name of the database to check, and a possible search key. Thus, the command getent passwd kaliuser1 will return the information from the user database regarding the user kaliuser1.
> 
> ```
> root@kali:~$ getent passwd kaliuser1
> kaliuser1:x:1001:1001:Kali User::/home/kaliuser1:/bin/bash
> ```

# 5.2.2. Modifying an Existing Account or Password

The following commands allow modification of the information stored in specific fields of the user databases:

+   - passwd—permits a regular user to change their password, which in turn, updates the /etc/shadow file.
+   - chfn—(Change Full Name), reserved for the super-user (root), modifies the GECOS, or "general information" field.
+   - chsh—(Change Shell) changes the user's login shell. However, available choices will be limited to those listed in /etc/shells; the administrator, on the other hand, is not bound by this restriction and can set the shell to any program chosen.
+   - chage—(Change AGE) allows the administrator to change the password expiration settings by passing the user name as an argument or list current settings using the -l user option.