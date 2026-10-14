to his or her environment can be placed in the .bashrc file. Additional scripts with similar names are sometimes used on a Linux distribution. Examples include the following:

+   - .bash_default, which is executed each time a bash shell is started
+   - .bash_login, which is executed each time a bash shell is started
+   - .bash_logout, which is executed each time a user closes a bash shell

You may find other scripts with similar names on your Linux distribution. In general, the names of these files describe when they are used. Consult your Linux vendor or try placing test commands in each file (see Chapter 14 for directions) if you are unsure of how the files are used. Figure 3-2 shows how a typical series of start-up scripts is executed when a user logs in to Linux.

```
/etc/profile → ~/.profile → /etc/bashrc → ~/.bashrc
                or
                ~/.bash_profile
```

# Figure 3-2 The process of executing start-up shell scripts

![](bbox=[0.12, 0.6, 0.18, 0.7])

Additional scripts are executed as part of the X Window System. For example, a user's home directory might contain a script file named .xclients or .xinitrc that the X Window System checks for and executes as the graphical system is started. One key difference to note, however, is that when a user logs in or starts a shell, the systemwide script files (such as /etc/profile) are executed, followed by the corresponding file in the user's home directory. But when starting the X Window System, the system default files (such as /etc/X11/xinit/xinitrc) are executed only if corresponding files are not found in the user's home directory. Chapter 15, "Advanced Topics and Troubleshooting," describes these issues in more depth.

The scripts described here apply when a bash shell is started. Similar files are executed when a user chooses to work with a C shell, Korn shell, or other shell. For example, a user's home directory may contain a file called .cshrc or .kshrc. These scripts are executed each time a C shell or Korn shell is started, respectively. Because the script format is different for each type of shell, different script files are needed to initialize each shell. These configuration scripts can coexist in a user's home directory (and in the /etc directory, for systemwide configuration files), each one being executed only when the corresponding shell is started.

# Using Aliases

An alias is a string of characters that is substituted for another string of characters at the shell prompt. The alias command lets you define how the shell will substitute one string of text for another string of text that you enter at a shell prompt. The general format of the alias command looks like this:

```
alias <string entered by user>=<string substituted by the shell>
```