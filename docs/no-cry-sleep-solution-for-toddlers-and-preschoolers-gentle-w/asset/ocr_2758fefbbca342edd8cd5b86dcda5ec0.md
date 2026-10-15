```
. /etc/bashrc
fi
set -o ignoreeof
set -o noclobber
alias rm='rm -i'
alias mv='mv -i'
alias cp='cp -i'
```

You can add any commands or definitions of your own to your .bashrc file. If you have made changes to .bashrc and you want them to take effect during your current login session, you need to reexecute the file with either the . or the source command.

```
$ .bashrc
```

# System /etc/.bashrc BASH Script

Linux systems usually contain a system .bashrc file executed for all users. This may contain certain global aliases and features needed by all users whenever they enter a BASH shell. This is located in the /etc directory, /etc/.bashrc. A user's own .bashrc file, located in the home directory, contains commands to execute this system .bashrc file. The ./etc/bashrc command in the previous example of .bashrc does just that.

# The BASH Shell Logout File: .bash_logout

The .bash_logout file is also a configuration file, which is executed when the user logs out. It is designed to perform any operations you want done whenever you log out. Instead of variable definitions, the .bash_logout file usually contains shell commands that form a kind of shutdown procedure—actions you always want taken before you log out. One common logout command is to clear the screen and then issue a farewell message.
As with .bash_profile, you can add your own shell commands to .bash_logout. In fact, the .bash_logout file is not automatically set up for you when your account is first created. You need to create it yourself, using the Vi or Emacs editor. You could then add a farewell message or other operations. In the next example, the user has a clear and an echo command in the .bash_logout file. When the user logs out, the clear command clears the screen, and then the echo command displays the message "Good-bye for now."

```
.bash_logout
# ~/ .bash_logout
clear
echo "Good-bye for now"
```

# Initialization and Configuration Files

Each type of shell has its own set of initialization and configuration files. The Bash shell configuration files were discussed previously. The TCSH shell uses .login, .tcshrc, .logout files in place of .bash_profile, .bashrc, and .bash_logout. The Z shell has several initialization files: .zshenv, .zlogin, .zprofile, .zshrc, and .zlogout. See Table 9-2 for a listing. Check the Man pages for each shell to see how they are usually configured. When you install a shell, default versions of these files are automatically placed in the users' home directories. Except for the TCSH shell, all shells use much the same syntax for variable definitions and assigning values (TCSH uses a slightly different syntax, described in its Man pages).