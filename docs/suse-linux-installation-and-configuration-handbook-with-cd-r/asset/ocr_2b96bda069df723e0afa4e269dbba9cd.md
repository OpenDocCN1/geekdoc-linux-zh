the shell will append the output to the file you specified. If you want to redirect error messages that are sent to the standard error, type the following:

```
$ command 2> file.txt
```

In the previous command, 2> redirects the standard error to the file you specify. You can combine both pipes and redirecting in the same command:

```
$ ls -l | sort +4n > sortedlist.txt
```

The previous will store the output of the piped commands in the file called sortedlist.txt.

# The Bash Shell

Bash is one of the best shells available for Linux and is the default shell in SuSE Linux. Bash offers several features that are available in other shells, and some features that are specific to Bash. Bash has features that were inspired by other shells such as the Korn shell, C shell, and Bourne shell. This makes bash a very powerful shell because it takes the best of all the shells and adds to it.

# Initialization Files

The bash shell reads special configuration files when it begins to configure itself: /etc/profile, .bash_profile, and .bashrc. Which files are read depends on how you run bash.

The first of these files is /etc/profile, which is discussed in earlier chapters. This file is the systemwide configuration file and is read by all users' shells when they start. This file is only writable by root, which uses it to declare system variables and scripts root wants to apply to all users in the system. Bash will read and execute all the commands found in /etc/profile whenever you run it as a login or interactive shell. An interactive shell is a shell you use to type commands in.

The second configuration file is .bash_profile, which resides in your home directory. This file is read by bash whenever you run it for login or interactive use. You can set any configurations for the shell you want in this file. In SuSE Linux, this file is named .profile. Despite its different name, it is the exact same file as .bash_profile.