pathname for your home directory. Commands such as cd reference the pathname in the HOME shell variable to locate your home directory. Some of the more common of these parameter variables are described in this section. Other parameter variables are defined by the system and given an initial value that you are free to change. To do this, you redefine them and assign a new value. For example, the PATH variable is defined by the system and given an initial value; it contains the pathnames of directories where commands are located. Whenever you execute a command, the shell searches for it in these directories. You can add a new directory to be searched by redefining the PATH variable yourself, so that it will include the new directory's pathname. Still other parameter variables exist that the system does not define. These are usually optional features, such as the EXINIT variable that enables you to set options for the Vi editor. Each time you log in, you must define and assign a value to such variables. Some of the more common parameter variables are SHELL, PATH, PS1, PS2, and MAIL. The SHELL variable holds the pathname of the program for the type of shell you log in to. The PATH variable lists the different directories to be searched for a Linux command. The PS1 and PS2 variables hold the prompt symbols. The MAIL variable holds the pathname of your mailbox file. You can modify the values for any of them to customize your shell.

> **NOTE** You can obtain a listing of the currently defined shell variables using the env command. The env command operates like the set command, but it lists only parameter variables.

# ### Using Initialization Files

You can automatically define parameter variables using special shell scripts called initialization files. An *initialization file* is a specially named shell script executed whenever you enter a certain shell. You can edit the initialization file and place in it definitions and assignments for parameter variables. When you enter the shell, the initialization file will execute these definitions and assignments, effectively initializing parameter variables with your own values. For example, the BASH shell's .bash_profile file is an initialization file executed every time you log in. It contains definitions and assignments of parameter variables. However, the .bash_profile file is basically only a shell script, which you can edit with any text editor such as the Vi editor; changing, if you wish, the values assigned to parameter variables.

In the BASH shell, all the parameter variables are designed to be environment variables. When you define or redefine a parameter variable, you also need to export it to make it an environment variable. This means any change you make to a parameter variable must be accompanied by an export command. You will see that at the end of the login initialization file, .bash_profile, there is usually an export command for all the parameter variables defined in it.

# ### Your Home Directory: HOME

The HOME variable contains the pathname of your home directory. Your home directory is determined by the parameter administrator when your account is created. The pathname for your home directory is automatically read into your HOME variable when you log in. In the next example, the echo command displays the contents of the HOME variable:

```
```
$ echo $HOME
/home/chris
```
```