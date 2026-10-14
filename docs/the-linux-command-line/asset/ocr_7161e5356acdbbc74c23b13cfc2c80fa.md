| Alt-n | Forward search, non-incremental. |
| Ctrl-o | Execute the current item in the history list and advance to the next one. This is handy if you are trying to re-execute a sequence of commands in the history list. |

# History Expansion

The shell offers a specialized type of expansion for items in the history list by using the "!" character. We have already seen how the exclamation point can be followed by a number to insert an entry from the history list. There are a number of other expansion features:

Table 9-6: History Expansion Commands

| Sequence | Action |
| !! | Repeat the last command. It is probably easier to press up arrow and enter. |
| !number | Repeat history list item number. |
| !string | Repeat last history list item starting with string. |
| !?string | Repeat last history list item containing string. |

I would caution against using the "!string" and "!?string" forms unless you are absolutely sure of the contents of the history list items.

There are many more elements available in the history expansion mechanism, but this subject is already too arcane and our heads may explode if we continue. The HISTORY EXPANSION section of the bash man page goes into all the gory details. Feel free to explore!

> **script**
> 
> In addition to the command history feature in bash, most Linux distributions include a program called script that can be used to record an entire shell session and store it in a file. The basic syntax of the command is:
> 
> `script [file]`