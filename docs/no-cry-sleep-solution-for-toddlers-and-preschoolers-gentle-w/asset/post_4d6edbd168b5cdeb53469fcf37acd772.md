
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

## System /etc/.bashrc BASH Script

Linux systems usually contain a system .bashrc file executed for all users. This may contain certain global aliases and features needed by all users whenever they enter a BASH shell. This is located in the /etc directory, /etc/.bashrc. A user's own .bashrc file, located in the home directory, contains commands to execute this system .bashrc file. The ./etc/bashrc command in the previous example of .bashrc does just that.

## The BASH Shell Logout File: .bash_logout

The .bash_logout file is also a configuration file, which is executed when the user logs out. It is designed to perform any operations you want done whenever you log out. Instead of variable definitions, the .bash_logout file usually contains shell commands that form a kind of shutdown procedure—actions you always want taken before you log out. One common logout command is to clear the screen and then issue a farewell message.

As with .bash_profile, you can add your own shell commands to .bash_logout. In fact, the .bash_logout file is not automatically set up for you when your account is first created. You need to create it yourself, using the Vi or Emacs editor. You could then add a farewell message or other operations. In the next example, the user has a clear and an echo command in the .bash_logout file. When the user logs out, the clear command clears the screen, and then the echo command displays the message "Good-bye for now."

```
.bash_logout
# ~/ .bash_logout
clear
echo "Good-bye for now"
```

## Initialization and Configuration Files

Each type of shell has its own set of initialization and configuration files. The Bash shell configuration files were discussed previously. The TCSH shell uses .login, .tcshrc, .logout files in place of .bash_profile, .bashrc, and .bash_logout. The Z shell has several initialization files: .zshenv, .zlogin, .zprofile, .zshrc, and .zlogout. See Table 9-2 for a listing. Check the Man pages for each shell to see how they are usually configured. When you install a shell, default versions of these files are automatically placed in the users' home directories. Except for the TCSH shell, all shells use much the same syntax for variable definitions and assigning values (TCSH uses a slightly different syntax, described in its Man pages).

## TABLE 9-2
Shell Configuration Files

| BASH Shell | Function |
|---|---|
| .bash_profile | Login initialization file |
| .bashrc | BASH shell configuration file |
| .bash_logout | Logout file |
| .bash_history | History file |
| /etc/profile | System login initialization file |
| /etc/bashrc | System BASH shell configuration file |
| /etc/profile.d | Directory for specialized BASH shell configuration files |
| TC SH Shell |  |
| .login | Login initialization file |
| .tcshrc | TC SH shell configuration file |
| .logout | Logout file |
| Z Shell |  |
| .zshenv | Shell login file (first read) |
| .zprofile | Login initialization file |
| .zlogin | Shell login file |
| .zshrc | Z shell configuration file |
| .zlogout | Logout file |
| PDKSH Shell |  |
| .profile | Login initialization file |
| .kshrc | PDKSH shell configuration file |

## Configuration Directories and Files

Applications often install configuration files in a user’s home directory that contain specific configuration information, which tailors the application to the needs of that particular user. This may take the form of a single configuration file that begins with a period, or a directory that contains several configuration files. The directory name will also begin with a period. For example, Mozilla installs a directory called .mozilla in the user’s home directory that contains configuration files. On the other hand, the Mail application uses a single file called .mailrc to hold alias and feature settings set up by the user. Most single configuration files end in the letters rc. FTP uses a file called .netrc. Most newsreaders use a file called .newsrc. Entries in configuration files are usually set by the application, though you can usually make entries directly by editing the file. Applications have their own set of special variables to which you can define and assign values. You can list the configuration files in your home directory with the ls -a command.
