Using the -v parameter when defining the tcsh shell in the script causes the shell to display each statement before executing it.

# The tcsh files

The tcsh shell automatically looks for several default files for setting environment variables and executing commands. If any of the default files exist, the tcsh shell executes them at specific instances. There are three different types of default files the tcsh shell can handle:

+   - Login files
- Shell startup files
- Logout files

This section examines the myriad of possible files you can use for your tcsh shell.

# The tcsh login files

If you use the tcsh as a login shell, it first looks for and executes the files:

+   - /etc/csh.login
- /etc/csh/login

You'll notice that all of these files use csh in the filename. Since the tcsh shell was designed as a replacement for the original C shell, it was designed to handle any of the default files that the C shell could. This made migrating from the C shell environment to the tcsh shell environment a snap.

These files are for all users who use the tcsh as their login shell. The files should contain system-wide environment variables that should be set for all users, and executable programs that all users should use (such as the umask command to set default file and directory permissions). Most likely if you're using a Linux distribution that supports the tcsh shell, one of these files already exists for setting system environment variables at login.

After executing either of these two files, the tcsh shell looks for a file in each user's $HOME directory:

```
$HOME/.login
```

This file can contain user-specific environment variable settings, and executable commands that an individual user wants to run when logging into the system, before the command interface prompt appears.

Any environment variable settings you make in the $HOME/.login shell will override system-wide settings made in the /etc/csh.login file. You can test the order in which the tcsh shell executes these files by adding a simple echo statement to each one, logging in: