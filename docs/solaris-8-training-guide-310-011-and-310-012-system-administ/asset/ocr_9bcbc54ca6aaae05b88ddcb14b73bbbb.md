# SUMMARY TABLE 24

# SOLARIS LP COMMANDS

| Command | Description |
|---|---|
| accept/reject | Enables or disables any further requests for a printer or class entering the spooling area. |
| cancel | Lets the user stop the printing of information. |
| enable/disable | Enables or disables any more output from the spooler to the printer. |
| lp | The user's print command. Places information to be printed into the spooler. |
| lpadmin | Allows the configuration of the print service. |
| lpmove | Moves print requests between destinations. |
| lpsched | Starts the print service. |
| lpshut | Stops the print service. |
| lpstat | Displays the status of the print service. |

| Utility | Description |
|---|---|
| pax | Copies files and directory subtrees to a single tape. This command provides better portability than tar or cpio, so it can be used to transport files to other types of UNIX systems. |
| ufsdump | Backs up all files in a file system. |
| ufsrestore | Restores some or all of the files archived with the ufsdump command. |

# WRITING SHELL SCRIPTS AND PROGRAMS

The Solaris 8 operating environment offers three commonly used shells:

+   - The Bourne shell (/sbin/sh). The default shell. It is a command programming language that executes commands read from a terminal or a file.
- The C shell (/bin/csh). A command interpreter with a C-like syntax. The C-shell provides a number of convenient features for interactive use that are not available with the Bourne shell, including filename completion, command aliasing, and history substitution.
- The Korn shell (/bin/ksh). A command programming language that executes commands read from a terminal or a file.

The login shell is the command interpreter that runs when you log in. The Solaris 8 operating environment offers the three most commonly used shells, as described in Summary Table 26.

# BACKUP AND RECOVERY

Solaris provides the utilities listed in Summary Table 25. They can be used to copy data from disk to removable media and restore it.

# SUMMARY TABLE 25

# BACKUP UTILITIES

| Utility | Description |
|---|---|
| tar | Archives data to another directory, system, or medium. |
| dd | Copies data quickly. |
| cpio | Copies data from one location to another. |