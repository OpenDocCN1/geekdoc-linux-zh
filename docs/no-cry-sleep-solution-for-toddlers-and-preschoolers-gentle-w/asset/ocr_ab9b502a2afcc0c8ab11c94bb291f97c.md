but also create the home directory for the user and install initialization files in the user's home directory.

These tools also let you control a user's access to their accounts. You can set expiration dates for users or lock them out of their accounts. Users locked out of their accounts will have their password in the /etc/shadow file prefixed by the invalid string, !. Unlocking the account removes this prefix.

> Tip With the Red Hat authentication tool (authconfig-gtk, see Chapter 4), you can enable and configure various authentication tools such as NIS and LDAP servers, as well as enabling shadow passwords, LDAP, and Kerberos authentication (accessible as Authentication on the System Settings menu and windows).

# Managing User Environments

Each time a user logs in, two profile scripts are executed, a system profile script that is the same for every user, and a user login profile script that can be customized to each user's needs. When the user logs out, a user logout script is run. In addition, each time a shell is generated, including the login shell, a user shell script is run. There are different kinds of scripts used for different shells. On Red Hat, the default shell commonly used is the BASH shell. As an alternative, users could use different shells such as TCSH or the Z shell, both installed with Red Hat Linux.

# Profile Scripts

For the BASH shell, each user has their own BASH login profile script named .bash_profile in their home directory. The system profile script is located in the /etc directory and named profile with no preceding period. The BASH shell user shell script is called .bashrc. The .bashrc file also runs the /etc/bashrc file to implement any global definitions such as the PS1 and TERM variables. The /etc/bashrc file also executes any specialized initialization file in the /etc/profile.d directory, such as those used for KDE and GNOME. The .bash_profile file runs the .bashrc file, and through it, the /etc/bashrc file, implementing global definitions. As a superuser, you can edit any of these profile or shell scripts and put in any commands you want executed for each user when they log in. For example, you may want to define a default path for commands, in case the user has not done so. Or you may want to notify the user of recent system news or account changes.

# /etc/skel

When you first add a user to the system, you must provide the user with skeleton versions of their login, shell, and logout initialization files. For the BASH shell, these would be the .bash_profile, .bashrc, and .bash_logout files. The useradd command and other user management tools such as Red Hat User Manager add these files automatically, copying any files in the directory /etc/skel to the user's new home directory. The /etc/skel directory contains a skeleton initialization file for the .bash_profile, .bashrc, and .bash_logout files or, if you are using the TCSH shell as your login shell, the .login, .tcshrc, and .logout files. The /etc/skel directory also contains default files and directories for your desktops. These