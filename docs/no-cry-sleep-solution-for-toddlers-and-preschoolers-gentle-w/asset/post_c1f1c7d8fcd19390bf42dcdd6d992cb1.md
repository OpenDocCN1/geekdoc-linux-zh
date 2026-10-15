
A reserved set of keywords is used for the names of these system variables. You should not use these keywords as the names of any of your own variable names. The system variables are all specified in uppercase letters, making them easy to identify. Shell feature variables are in lowercase letters. For example, the keyword HOME is used by the system to define the HOME variable. HOME is a special environment variable that holds the pathname of the user’s home directory. On the other hand, the keyword noclobber is used to set the noclobber feature on or off.

## System Variables

Many of the system variables automatically defined and assigned initial values by the system when you log in can be changed, if you wish. Some system variables exist whose values should not be changed, however. For example, the HOME variable holds the pathname for your home directory. Commands such as cd reference the pathname in the HOME system variable to locate your home directory. Some of the more common of these system variables are described in this section. Other system variables are defined by the system and given an initial value that you are free to change. To do this, you redefine them and assign a new value. For example, the PATH variable is defined by the system and given an initial value; it contains the pathnames of directories where commands are located. Whenever you execute a command, the shell searches for it in these directories. You can add a new directory to be searched by redefining the PATH variable yourself, so that it will include the new directory’s pathname. Still other special variables exist that the system does not define. These are usually optional features, such as the EXINIT variable that enables you to set options for the Vi editor. Each time you log in, you must define and assign a value to such variables. Some of the more common system variables are SHELL, PATH, PS1, PS2, and MAIL. The SHELL variable holds the pathname of the program for the type of shell you log in to. The PATH variable lists the different directories to be searched for a Linux command. The PS1 and PS2 variables hold the prompt symbols. The MAIL variable holds the pathname of your mailbox file. You can modify the values for any of them to customize your shell.

> **NOTE** You can obtain a listing of the currently defined system variables using the env command. The env command operates like the set command, but it lists only system variables.

### Using Initialization Files

You can automatically define system variables using special shell scripts called initialization files. An initialization file is a specially named shell script executed whenever you enter a certain shell. You can edit the initialization file and place in it definitions and assignments for system variables. When you enter the shell, the initialization file will execute these definitions and assignments, effectively initializing system variables with your own values. For example, the BASH shell’s .bash_profile file is an initialization file executed every time you log in. It contains definitions and assignments of system variables. However, the .bash_profile file is basically only a shell script, which you can edit with any text editor such as the Vi editor; changing, if you wish, the values assigned to system variables.

In the BASH shell, all the system variables are designed to be environment variables. When you define or redefine a system variable, you also need to export it to make it an environment variable. This means any change you make to a system variable must be accompanied by an export command. You will see that at the end of the login initialization file, .bash_profile, there is usually an export command for all the system variables defined in it.

### Your Home Directory: HOME

The HOME variable contains the pathname of your home directory. Your home directory is determined by the system administrator when your account is created. The pathname for your home directory is automatically read into your HOME variable when you log in. In the next example, the echo command displays the contents of the HOME variable:

```
$ echo $HOME
/home/chris
```

The HOME variable is often used when you need to specify the absolute pathname of your home directory. In the next example, the absolute pathname of reports is specified using HOME for the home directory's path:

```
$ ls $HOME/reports
```

### Command Locations: PATH

The PATH variable contains a series of directory paths separated by colons. Each time a command is executed, the paths listed in the PATH variable are searched one by one for that command. For example, the cp command resides on the system in the directory /usr/bin. This directory path is one of the directories listed in the PATH variable. Each time you execute the cp command, this path is searched and the cp command is located. The system defines and assigns PATH an initial set of pathnames. In Linux, the initial pathnames are /usr/bin and /usr/sbin.

The shell can execute any executable file, including programs and scripts you have created. For this reason, the PATH variable can also reference your working directory; so if you want to execute one of your own scripts or programs in your working directory, the shell can locate it. No spaces are allowed between the pathnames in the string. A colon with no pathname specified references your working directory. Usually, a single colon is placed at the end of the pathnames as an empty entry specifying your working directory. For example, the pathname /usr/bin:/usr/sbin: references three directories: /usr/bin, /usr/sbin, and your current working directory.

```
$ echo $PATH
/usr/bin:/usr/sbin:
```
