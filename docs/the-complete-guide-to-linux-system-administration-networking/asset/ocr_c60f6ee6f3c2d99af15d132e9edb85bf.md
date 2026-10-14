+   - A new user is created with the same user name as the deleted user, and e-mail intended for the previous user is dropped in the e-mail box of the new user.
+   - A new user is created with the same UID as the previous user and some files remained from the previous user that have that UID listed as the owner. The new user with the same UID will have access to those files (effectively, he or she will own them).

You can think about these issues and decide for yourself whether to delete user accounts or simply disable them (as described shortly).

# Creating New Users at the Command Line

The basic command-line utility for creating new users is useradd. With this utility you can create new accounts using many different options, and even automate user creation in scripts.

> On some Linux systems, including Red Hat Linux and Fedora, a command named adduser is available. This is simply a symbolic link to the useradd command.

To add a user with useradd, you must be logged in as root. You provide the name of the new user account as a parameter. For example, to add a new account called r Solomon, you use this command:

```
# useradd rSolomon
```

System defaults are used to create the account and a home directory. These system defaults are stored in the /etc/login.defs file and in the /etc/default/useradd file.

You can add options to the useradd command to override the system default settings or include more user information as part of the account configuration. For example, if you want to include the user's full name in the comment field (generally a good idea), you can use the -c option. The -g option defines a primary group for the new user. A command incorporating these two options looks like this:

```
# useradd -g sales -c "Raley Solomon" rSolomon
```

> Values that include spaces, such as "Raley Solomon" in the above example, must be enclosed in quotation marks so the useradd command does not interpret the part after the space (Solomon) as a command parameter.

Table 11-1 shows options you can use when executing useradd.