Although you can pass options and arguments to commands, not all commands need to have arguments or options supplied on the command line to work properly. The date command is one example that simply prints the current date and time:

```
```
[root@server1 root]$ date
Tue Mar 29 08:58:36 EST 2005
[root@server1 root]_
```
```

Table 3-3 lists some common commands that you can use without specifying any options or arguments.

**Table 3-3** Some common Linux commands
| **Command** | **Description** |
| :--- | :--- |
| clear | Clears the terminal screen |
| reset | Resets your terminal to use default terminal settings |
| finger | Displays information on system users |
| who | Displays currently logged-in users |
| w | Displays currently logged-in users and their tasks |
| whoami | Displays your login name |
| id | Displays the numbers associated with your user account name and group names; these are commonly referred to as User IDs (UIDs) and Group IDs (GIDs) |
| date | Displays the current date and time |
| cal | Displays the calendar for the current month |
| exit | Exits out of your current shell |

If the output of a certain command is too large to fit on the terminal screen, simply use the Shift and Page Up keys simultaneously to view previous screens of information. Also, Shift and Page Down can be used to navigate in the opposite direction when pressed simultaneously.

You can recall commands previously entered in the BASH shell using the keyboard cursor keys (the up, down, right, and left arrow keys). Thus, if you want to enter the same command again, simply cycle through the list of available commands with the keyboard cursor keys and press Enter to reexecute that command.