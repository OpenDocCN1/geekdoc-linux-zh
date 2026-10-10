![](bbox=[0.14, 0.12, 0.23, 0.19])

The shift command shifts the parameter variables, so that what would ordinarily be $2 becomes $1, what would be $3 becomes $2, and so on. Adding a number, as in shift 3, shifts the assignments by that number of units. The shift command does not alter the $0 variable, though.

As an example of how a script with a parameter variable can help in such situations, consider Listing 9.2. This script creates an account and changes the account’s password (you’ll be prompted to enter the password when you run the script). It creates a directory in the /shared directory tree corresponding to the account, and it sets a symbolic link to that directory from the new user’s home directory. It also adjusts ownership and permissions in a way that may be useful, depending on your system’s ownership and permissions policies.

# **Listing 9.2: A Script That Reduces Account-Creation Tedium**

```
#!/bin/sh
useradd -m $1
passwd $1

mkdir -p /shared/$1
chown $1.users /shared/$1
chmod 775 /shared/$1

ln -s /shared/$1 /home/$1/shared
chown $1.users /home/$1/shared
```

If you use Listing 9.2, you need type only three things: the script name with the desired username and the password (twice). For instance, if the script is called mkuser, you can use it like this:

```
# mkuser ajones
Changing password for user ajones
New password:
Retype new password:
passwd: all authentication tokens updated successfully
```

Most of the scripts’ programs operate silently unless they encounter problems, so the interaction (including typing the passwords, which don’t echo to the screen) is a result of just the passwd command. In effect, Listing 9.2’s script replaces seven lines of commands with one. Every one of those lines uses the username, so by running this script, you also reduce the chance of a typo causing problems.

Another type of variable is assigned within scripts—for instance, such variables can be set from the output of a command. These variables are also identified by leading dollar signs, but they’re typically given names that at least begin with a letter, such as $addr or $name. (When values are assigned to variables, the dollar sign is omitted, as illustrated shortly.) You can then use these variables in conjunction with normal commands as if they were command parameters, but the value of the variable is passed to the command.