
- Use the history number.
- Use the beginning of a command.
- Search the history list.

The term “history number” refers to the number to the left of each item in the history list. For example, in the preceding history list, the first item has a history number of 33.

You can execute any of the commands in the history list by entering the number of that command prefixed by an exclamation point. An exclamation point is sometimes called a bang in UNIX and Linux. So to execute the most recent mount command in our example, you enter !41 (pronounced “bang forty-one”).

The shell displays the command matching that number and immediately executes it. You don’t need to view the history list before using this technique if you already know the number of the command you want to execute. But be aware that the numbers change as you enter new commands.

To use the command name to repeat a command, use an exclamation point followed by the first part of the command you want to repeat. In the sample history output shown, you could execute the most recent mount command using this command:

```
# !mou
```

When you execute this command, the shell searches for the most recent command that begins with the letters “mou” and executes it.

![](img/43f64015de86d989e30eff5bb284fb96_144_0.png)

When executing a command from the history list using any of the three methods described, remember that the commands are executed from your current working directory, which may be different from the directory where they were originally executed. If a command does not include a full pathname, you might see unexpected results. Be especially careful when using the partial command name method to reexecute a command without checking the full text of the command.

You can also search the history list without reexecuting a command to see what the command parameters were or how you completed a task. This method requires the use of a pipe symbol ( | ) and the grep command, which are discussed later in this chapter and in Chapter 5, “Understanding Text Processing.” To use this method, enter the history command, then a pipe symbol, then the grep command and the command name you want to locate. For example, in the sample history output shown previously, suppose you want to search for a mount command to see what parameters it contains. The following command displays all items in the history list that contain the mount command. You can then review the displayed output to learn about the previously executed command.

```
# history | grep mount
```

The bash shell supports additional techniques for executing commands. But the examples shown here for using tab completion and the history command should help you enter commands much more efficiently in Linux. To learn more about these features, review the online manual page for the bash shell by entering man bash.

## The Shell Start-up Process

Several scripts are executed when you log in to Linux or start a new shell. These scripts initialize (or configure) various parts of your environment.

When a user first logs in to a Linux system, the script /etc/profile is executed. The /etc/profile script contains configuration information that applies to every user on the system. Each user’s home directory can contain another start-up script called .profile (with an initial period). The .profile script in a user’s home directory is also executed when the user logs in, but the .profile script is specific to a single user. Each user’s home directory can contain a different profile script. Only the root user can change the /etc/profile script; any user can change the .profile script in his or her home directory.

![](img/43f64015de86d989e30eff5bb284fb96_145_0.png)

> Any file name in Linux that begins with a period is a hidden file. This is less a security feature and more a convenience to keep files out of the way when they are seldom changed. To see a list of files that includes all hidden files, use the -a option with the ls command. Within your home directory, the command ls -a produces a long list of hidden configuration files.

On some systems, additional scripts are executed when a user logs in. For example, in Red Hat Linux, a set of scripts located in the /etc/profile.d directory is started by the /etc/profile script. The scripts in the /etc/profile.d directory add specific configuration information for many different Linux programs. Red Hat Linux also uses a file called .bash_profile rather than the standard .profile script in each user’s home directory.

The profile scripts are executed when a user logs in; additional scripts are executed when a user starts a shell. Because a shell is started immediately when a user logs in at a text-mode screen, these additional scripts are generally executed immediately after the profile scripts. A user working in a graphical environment can start multiple bash shells without logging in to Linux again. When a new shell is started by a user who is already logged in, the additional scripts described next (such as /etc/bashrc) are executed; however, the profile scripts are not executed again.

Some Linux distributions, including Red Hat Linux, provide an /etc/bashrc script that is executed for all users on the system each time a bash shell is started. Other Linux distributions rely on the /etc/profile script for configuration settings that should apply to all users, though this script is only executed at the time a user logs in.

Each user’s home directory contains a script called .bashrc. The .bashrc script is executed each time the user starts a bash shell. Any configuration information that a user wants to add to his or her environment can be placed in the .bashrc file. Additional scripts with similar names are sometimes used on a Linux distribution. Examples include the following:

- .bash_default, which is executed each time a bash shell is started
- .bash_login, which is executed each time a bash shell is started
- .bash_logout, which is executed each time a user closes a bash shell

You may find other scripts with similar names on your Linux distribution. In general, the names of these files describe when they are used. Consult your Linux vendor or try placing test commands in each file (see Chapter 14 for directions) if you are unsure of how the files are used. Figure 3-2 shows how a typical series of start-up scripts is executed when a user logs in to Linux.

```
/etc/profile → ~/.profile → /etc/bashrc → ~/.bashrc
                or
                ~/.bash_profile
```

### Figure 3-2 The process of executing start-up shell scripts

![](img/43f64015de86d989e30eff5bb284fb96_146_0.png)

Additional scripts are executed as part of the X Window System. For example, a user's home directory might contain a script file named .xclients or .xinitrc that the X Window System checks for and executes as the graphical system is started. One key difference to note, however, is that when a user logs in or starts a shell, the systemwide script files (such as /etc/profile) are executed, followed by the corresponding file in the user's home directory. But when starting the X Window System, the system default files (such as /etc/X11/xinit/xinitrc) are executed only if corresponding files are not found in the user's home directory. Chapter 15, "Advanced Topics and Troubleshooting," describes these issues in more depth.

The scripts described here apply when a bash shell is started. Similar files are executed when a user chooses to work with a C shell, Korn shell, or other shell. For example, a user's home directory may contain a file called .cshrc or .kshrc. These scripts are executed each time a C shell or Korn shell is started, respectively. Because the script format is different for each type of shell, different script files are needed to initialize each shell. These configuration scripts can coexist in a user's home directory (and in the /etc directory, for systemwide configuration files), each one being executed only when the corresponding shell is started.

## Using Aliases

An alias is a string of characters that is substituted for another string of characters at the shell prompt. The alias command lets you define how the shell will substitute one string of text for another string of text that you enter at a shell prompt. The general format of the alias command looks like this:

```
alias <string entered by user>=<string substituted by the shell>
```
