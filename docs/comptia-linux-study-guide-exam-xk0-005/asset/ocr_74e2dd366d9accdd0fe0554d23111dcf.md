+   - .bash_login

+   - .profile

Typically, the fourth file, .bashrc, is run from the file found in the preceding list. However, any time a noninteractive shell is started, the .bashrc file is run.

In Listing 10.25, on a Rocky Linux distribution, the user's directory is checked for all four environment files. Notice that two of them are not found. Therefore, only the .bash_profile and .bashrc files are employed on this system.

# Listing 10.25: Reviewing a user account’s environment files

```
$ pwd
/home/Christine
$ ls .bash_profile .bash_login .profile .bashrc
ls: cannot access '.bash_login': No such file or directory
ls: cannot access '.profile': No such file or directory
.bash_profile .bashrc
$ 
```

![](bbox=[0.15, 0.44, 0.2, 0.49])

When referring to a user account's environment files, often symbols for environment files denoting the user's home directory are employed. For example, you may see the .bashrc environment file referred to as the $HOME/.bashrc or the ~/.bashrc file.

If you want to modify your shell's primary prompt ($PS1) persistently, you can do so by adding the modification to one of your local environment configuration files. Listing 10.26 shows the $PS1 variable's modification on a Fedora Workstation distribution.

# Listing 10.26: Persistently setting a user account’s shell prompt

```
$ grep PS1 .bash_profile
PS1="To infinity and beyond: "
$ 
```

Notice in Listing 10.26 that the user’s prompt is still set to a $. The new prompt designated in the $HOME/.bash_profile file will not take effect until the file is run, which can be done manually or automatically when the user logs out and back into the shell.

These individual user environment files are typically populated from the /etc/skel directory, depending on your account creation configuration scripts. For future accounts, you can make changes to the skeleton environment files. Just keep in mind that any individual user who can access the command line has the ability to modify their own files. Thus, for environment configurations that need to apply to all users, it is better to make a global entry in one of the global environment files, which are covered next.