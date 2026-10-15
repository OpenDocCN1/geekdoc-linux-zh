# Editing Your BASH Profile Script

Your .bash_profile initialization file is a text file that can be edited by a text editor, like any other text file. You can easily add new directories to your PATH by editing .bash_profile and using editing commands to insert a new directory pathname in the list of directory pathnames assigned to the PATH variable. You can even add new variable definitions. If you do so, however, be sure to include the new variable's name in the export command's argument list. For example, if your .bash_profile file does not have any definition of the EXINIT variable, you can edit the file and add a new line that assigns a value to EXINIT. The definition EXINIT='set nu ai' will configure the Vi editor with line numbering and indentation. You then need to add EXINIT to the export command's argument list. When the .bash_profile file executes again, the EXINIT variable will be set to the command set nu ai. When the Vi editor is invoked, the command in the EXINIT variable will be executed, setting the line number and auto-indent options automatically.

In the following example, the user's .bash_profile has been modified to include definitions of EXINIT and redefinitions of PATH, PS1, and HISTSIZE. The PATH variable has $HOME added to its value. $HOME is a variable that evaluates to the user's home directory, and the ending colon specifies the current working directory, enabling you to execute commands that may be located in either the home directory or the working directory. The redefinition of HISTSIZE reduces the number of history events saved, from 1,000 defined in the system's .profile file, to 30. The redefinition of the PS1 system variable changes the prompt to include the pathname of the current working directory. Any changes you make to system variables within your .bash_profile file override those made earlier by the system's .profile file. All these system variables are then exported with the export command.

```
.bash_profile
# .bash profile
# Get the aliases and functions
if [ -f ~/.bashrc ];
then
  ~/.bashrc
fi
# User-specific environment and startup programs
PATH=$PATH:$HOME/bin:$HOME:
BASH_ENV=$HOME/.bashrc
USERNAME="$"
HISTSIZE=30
NTP SERVER=ntp.myserver.com
EXINIT='set nu ai'
PS1="\w $"
export USERNAME BASH_ENV PATH HISTSIZE EXINIT PS1
```

# Manually Reexecuting the .bash_profile Script

Although .bash_profile is executed each time you log in, it is not automatically reexecuted after you make changes to it. The .bash_profile file is an initialization file that is executed only whenever you log in. If you want to take advantage of any changes you make to it without having to log out and log in again, you can reexecute .bash_profile with the dot (.) command. The .bash_profile file is a shell script and, like any shell script, can be executed with the . command.

```
$ .bash_profile
```