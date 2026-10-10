
## Command Reference

| Command | Description |
| :--- | :--- |
| sed | Streams line editing using editor commands |
| setterm | Modifies terminal settings |
| sleep | Pauses Bash shell operation for a specified amount of time |
| sort | Organizes data in a data file based on the specified order |
| stat | Views the file statistics of the specified file |
| sudo | Runs an application as the root user account |
| tail | Displays the last portion of the specified file's contents |
| tar | Archives data and directories into a single file |
| tee | Sends information to both STDOUT and STDIN |
| top | Displays the active processes, showing vital system statistics |
| touch | Creates a new empty file or updates the time stamp on an existing file |
| umount | Removes a mounted disk device from the virtual filesystem |
| uptime | Displays information on how long the system has been running |
| useradd | Creates a new system user account |
| userdel | Removes an existing system user account |
| usermod | Modifies an existing system user account |
| vgchange | Activates or deactivates an LVM volume group |
| vgcreate | Creates an LVM volume group |
| vgdisplay | Displays an LVM volume group |
| vgextend | Increases the size of an LVM volume group |
| vgreduce | Decreases the size of an LVM volume group |
| vgremove | Deletes an LVM volume group |
| vi | Invokes the vim text editor |
| vim | Invokes the vim text editor |
| wc | Displays text file statistics |
| whereis | Displays a designated command's files, including binary, source code, and man pages |
| which | Finds the location of an executable file |
| who | Displays users currently logged into system |
| whoami | Displays the current user's username |
| xargs | Takes items from STDIN, builds commands, and executes the commands |
| xterm | Invokes the xterm terminal emulator |
| zenity | Creates window widgets for GNOME Shell |
| zip | Unix version of the Windows PKZIP program |

You can accomplish just about any task you need to on the command line by using these commands.

## Assessing Environment Variables

The Bash shell also utilizes many environment variables. Although environment variables aren't commands, they often affect how shell commands operate, so it's important to know some of the shell environment variables. Table A.3 shows several of the environment variables available in the Bash shell.

**TABLE A.3** Bash Shell Environment Variables

| Variable | Description |
| :--- | :--- |
| * | Contains all the command line parameters as a single text value |
| @ | Contains all the command line parameters as separate text values |
| # | The number of command line parameters |
| ? | The exit status of the most recently used foreground process |
| - | The current command line option flags |
| $ | The process ID (PID) of the current shell |
| ! | The PID of the most recently executed background process |
| 0 | The name of the command from the command line |
| $0 | The name of the command from the command line |
| $SHELL | The absolute pathname of the shell |
| BASH | The full filename used to invoke the shell |
| BASHOPTS | Enabled shell options in a colon separated list |
| BASHPID | The current Bash shell's PID |
| BASH_ALIASES | An array containing the currently used aliases |
| BASH_ARGC | The number of parameters in the current subroutine |
| BASH_ARGV | An array containing all the command line parameters specified |
| BASH_CMDS | An array containing the internal hash table of commands |
| BASH_COMMAND | The name of the command currently being executed |
| BASH_ENV | When set, each Bash script attempts to execute a startup file defined by this variable before running. |
| BASH_EXECUTION_STRING | The command used in the -c command line option |
| BASH_LINENO | An array containing the line numbers of each command in the script |
| BASH_REMATCH | An array containing text elements that match a specified regular expression |
| BASH_SOURCE | An array containing source filenames for |
| BASH_SUBSHELL | The number of subshells spawned by the current shell |
| BASH_VERSINFO | A variable array that contains the individual major and minor version numbers of the current instance of the Bash shell |
| BASH_VERSION | The version number of the current instance of the Bash shell |
| BASH_XTRACEFD | When set to a valid file descriptor integer, trace output is generated and separated from diagnostic and error messages. The file descriptor must have set -x enabled. |
| BROWSER | The absolute pathname of the preferred web browser |
| COLUMNS | Contains the terminal width of the terminal used for the current instance of the Bash shell |
| COMP_CWORD | An index into the variable COMP_WORDS, which contains the current cursor position |
| COMP_KEY | The completion invocation character keyboard key |
| COMP_LINE | The current command line |
| COMP_POINT | The index of the current cursor position relative to the beginning of the current command |
| COMP_TYPE | The completion type integer value |
| COM_WORDBREAKS | A set of characters used as word separators when performing word completion |
| COMP_WORDS | A variable array that contains the individual words on the current command line |
| COMPREPLY | A variable array that contains the possible completion codes generated by a shell function |
| COPROC | A variable array that holds file descriptors for an unnamed coprocess's I/O |
| DBUS_SESSION_BUS_ADDRESS | The current login session's D-Bus address that provides a map for connections |
| DE | A variable that contains the current login session's desktop environment |
| DESKTOP_SESSION | Within an LXDE environment, a variable that contains the current login session's desktop environment |
| DIRSTACK | A variable array that contains the current contents of the directory stack |
| DISPLAY | A variable that contains a map for graphical applications for where to display the graphical user interface |
| EDITOR | When set, defines the default editor used by some shell commands |
| EMACS | When set, the shell assumes it's running in an Emacs shell buffer and disables line editing. |
| ENV | When the shell is invoked in POSIX mode, each Bash script attempts to execute a startup file defined by this variable before running. |
| EUID | The numeric effective user ID of the current user |
| FCEDIT | The default editor used by the fc command |
| FIGNORE | A colon-separated list of suffixes to ignore when performing filename completion |
| FUNCNAME | The name of the currently executing shell function |
| FUNCNEST | The maximum level for nesting functions |
| GLOBIGNORE | A colon,separated list of patterns defining the set of filenames to be ignored by filename expansion |
| GROUPS | A variable array containing the list of groups of which the current user is a member |
| histchars | Up to three characters that control history expansion |
| HISTCMD | The history number of the current command |
| HISTCONTROL | Controls what commands are entered in the shell history list |
| HISTFILE | The name of the file to save the shell history list (~/.bash_history by default) |
| HISTFILESIZE | The maximum number of lines to save in the history file |
| HISTIGNORE | A colon,separated list of patterns used to decide which commands are ignored for the history file |
| HISTSIZE | The maximum number of commands stored in the history file |
| HISTTIMEFORMAT | When set, determines the format string for the history file entries' time stamps |
| HOME | Current login session's home directory name |
| HOSTALIASES | Contains the name of the file that holds aliases for various host names used by some shell commands |
| HOSTFILE | Contains the name of the file that should be read when the shell needs to complete a host name |
| HOSTNAME | The name of the current host |
| HOSTTYPE | A string describing the machine the Bash shell is running on |
| IFS | Contains a list of characters used to separate files, when the words are split as part of an expansion |
| IGNOREEOF | The number of consecutive EOF characters the shell must receive before exiting. If this value doesn't exist, the default is 1. |
| INFODIR | A colon,separated list of info page directories searched by the `info` command |
| INPUTRC | The name of the readline initialization file. The default is `~/.inputrc`. |
| INVOCATION_ID | A random and unique 128 bit identifier used to identify login shells (and other units) by `systemd` |
| JOURNAL_STREAM | A colon,separated list of a file descriptor's device and inode number (in decimal format). This is set only when `STDOUT` or `STDERR` are connected to the journaling system. |
| LANG | The locale category for the shell |
| LC_ALL | Overrides the `LANG` variable, defining a locale category |
| LC_ADDRESS | Determines how address information is displayed |
| LC_COLLATE | Sets the collation order used when sorting string values |
| LC_CTYPE | Determines the interpretation of characters used in filename expansion and pattern matching |
| LC_IDENTIFICATION |  |
