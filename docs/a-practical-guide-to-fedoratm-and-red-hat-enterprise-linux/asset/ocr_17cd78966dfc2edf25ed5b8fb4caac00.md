# **history** can help track down mistakes

> **tip** When you have made a mistake on a command line (not an error within a script or program) and are not sure what you did wrong, look at the history list to review your recent commands. Sometimes this list can help you figure out what went wrong and how to fix things.

The **history** builtin displays the history list. If it does not, read the next section, which describes the variables you might need to set.

# VARIABLES THAT CONTROL HISTORY

The value of the **HISTSIZE** variable determines the number of events preserved in the history list during a session. A value in the range of 100 to 1,000 is normal.

When you exit from the shell, the most recently executed commands are saved in the file whose name is stored in the **HISTFILE** variable (default is `~/.bash_history`). The next time you start the shell, this file initializes the history list. The value of the **HISTFILESIZE** variable determines the number of lines of history saved in **HISTFILE** (see Table 9-7).

Table 9-7 History variables
| Variable | Default | Function |
| :--- | :--- | :--- |
| **HISTSIZE** | 1,000 events | Maximum number of events saved during a session |
| **HISTFILE** | `~/.bash_history` | Location of the history file |
| **HISTFILESIZE** | 1,000 events | Maximum number of events saved between sessions |

Event number The Bourne Again Shell assigns a sequential **event number** to each command line. You can display this event number as part of the **bash** prompt by including `!` in **PS1** (page 361). Examples in this section show numbered prompts when they help to illustrate the behavior of a command.

Enter the following command manually to establish a history list of the 100 most recent events; place it in `~/.bash_profile` to affect future sessions:

```
$ **HISTSIZE=100**
```

The following command causes **bash** to save the 100 most recent events across login sessions:

```
$ **HISTFILESIZE=100**
```

After you set **HISTFILESIZE**, you can log out and log in again, and the 100 most recent events from the previous login session will appear in your history list.

Enter the command **history** to display the events in the history list. This list is ordered with the oldest events at the top. The following history list includes a command to