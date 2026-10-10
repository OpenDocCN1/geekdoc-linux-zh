# Appendix A: Quick Guide to Bash Commands

You can accomplish just about any task you need to on the command line by using these commands.

# Assessing Environment Variables

The Bash shell also utilizes many environment variables. Although environment variables aren’t commands, they often affect how shell commands operate, so it’s important to know some of the shell environment variables. Table A.3 shows several of the environment variables available in the Bash shell.

TABLE A.3  **Bash Shell Environment Variables**

| Variable | Description |
| :--- | :--- |
| * | Contains all the command-line parameters as a single text value. |
| @ | Contains all the command-line parameters as separate text values. |
| # | The number of command-line parameters. |
| ? | The exit status of the most recently used foreground process. |
| - | The current command-line option flags. |
| $ | The process ID (PID) of the current shell. |
| ! | The PID of the most recently executed background process. |
| 0 | The name of the command from the command line. |
| _ | The absolute pathname of the shell. |
| BASH | The full filename used to invoke the shell. |
| BASHOPTS | Enabled shell options in a colon-separated list. |
| BASHPID | The current Bash shell’s PID. |
| BASH_ALIASES | An array containing the currently used aliases. |
| BASH_ARGC | The number of parameters in the current subroutine. |
| BASH_ARGV | An array containing all the command-line parameters specified. |
| BASH_CMDS | An array containing the internal hash table of commands. |
| BASH_COMMAND | The name of the command currently being executed. |
| BASH_ENV | When set, each Bash script attempts to execute a startup file defined by this variable before running. |
| BASH_EXECUTION_STRING | The command used in the `-c command-line option. |
| BASH_LINENO | An array containing the line numbers of each command in the script. |
| BASH_REMATCH | An array containing text elements that match a specified regular expression. |
| BASH_SOURCE | An array containing source filenames for the declared functions in the shell. |