# ## Aliases

bash provides the ability to create an alias for a command. The syntax is as follows:

```
alias new_name=command
```

Aliases with command-line options should be surrounded by quotes, such as in the following:

```
alias home='cd /home/jason'
```

Aliases can also point to other aliases, but in case of a loop, bash knows to execute the loop only one time.

![](bbox=[0.13, 0.35, 0.2, 0.4])

Many Linux distributions have aliases set up to help the user migrating from other operating systems, mainly MS-DOS.

![](bbox=[0.13, 0.43, 0.2, 0.49])

It may seem like a good idea to use an alias for frequently misspelled commands, but it is better to learn the real command. For example, many Linux distributions alias `cd..` to `cd ..`, but you should learn the correct command, because you cannot always count on the alias being set.

# ## Special files

There are several script files that get run at login, when starting a new shell, or when logging out. These script files help set up and configure the shell environment automatically for the user. These files are the following:

+   - `.bash_profile`
+   - `.bashrc`
+   - `.profile`
+   - `/etc/profile`
+   - `.bash_logout`
+   - `.inputrc`
+   - `/etc/inputrc`

# ## Login files

When a user logs into the system, the user is given a shell, which is known as a *login shell*. When a user starts another instance of a shell from the command-line or within the X Window system, that is a *nologin shell*. This is important because some files are read only in certain circumstances. During a login shell, the shell reads the `/etc/profile` file, if it exists. After that it checks for the following files in order and stops looking after the first one is found.