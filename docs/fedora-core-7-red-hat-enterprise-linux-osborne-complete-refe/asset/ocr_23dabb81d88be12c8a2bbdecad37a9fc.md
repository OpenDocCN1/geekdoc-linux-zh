| Command (CTRL-R for listing possible completions) | Description |
| :--- | :--- |
| TAB | Automatic completion |
| TAB TAB OF ESC | List possible completions |
| ALT-/, CTRL-R-/ | Filename completion, normal text for automatic |
| ALT-$, CTRL-R-$ | Shell variable completion, $ for automatic |
| ALT-~, CTRL-R-~ | User name completion, ~ for automatic |
| ALT-@, CTRL-R-@ | Host name completion, @ for automatic |
| ALT-!, CTRL-R-! | Command name completion, normal text for automatic |

**TABLE 8-3** Command Line Editing Operations

> **TIP** *The capability to redisplay a previous command is helpful when you've already executed a command you had entered incorrectly. In this case, you would be presented with an error message and a new, empty command line. By pressing the UP ARROW key, you can redisplay your previous command, make corrections to it, and then execute it again. This way, you would not have to enter the whole command again.*

# History Events

In the BASH shell, the *history* utility keeps a record of the most recent commands you have executed. The commands are numbered starting at 1, and a limit exists to the number of commands remembered—the default is 500. The history utility is a kind of short-term memory, keeping track of the most recent commands you have executed. To see the set of your most recent commands, type `history` on the command line and press ENTER. A list of your most recent commands is then displayed, preceded by a number.

```
$ history
1 cp mydata today
2 vi mydata
3 mv mydata reports
4 cd reports
5 ls
```

Each of these commands is technically referred to as an event. An *event* describes an action that has been taken—a command that has been executed. The events are numbered according to their sequence of execution. The most recent event has the highest number. Each of these events can be identified by its number or beginning characters in the command.

The history utility enables you to reference a former event, placing it on your command line and enabling you to execute it. The easiest way to do this is to use the UP ARROW and DOWN ARROW keys to place history events on your command line, one at a time. You needn't display the list first with `history`. Pressing the UP ARROW key once places the last history