The s indicates that this is a search operation, the % means that the entire file is to be searched, "Down" is the pattern to be found, "Up" is the new pattern, and the g tells vi that the search should continue until there are no more pattern matches. Without the g, vi would perform the replacement on only the first match it finds. This command also works with regular expressions appearing in the search pattern and the replacement pattern.

# ## Setting Preferences

vi is *configurable*, which means that you can set options to control your editing environment. These options are initialized with default values that you can modify in vi at any time. vi is configured using the set command. The set command must be preceded by a colon and entered by pressing Return. For example, to display line numbers in the editor, enter

```
:set number
```

The following table describes a few of the more common set commands.

| Option | Description |
| :--- | :--- |
| all | Displays a list of all available set options and their current status |
| errorbells | Sounds the terminal bell when an error occurs |
| ignorecase | Searches are case-insensitive |
| number | Displays line numbers in the leftmost column of the screen (these are not written to the file) |
| showmode | An indicator appears at the bottom right of the screen if you are in input mode, change mode, replace mode, and so on |

set commands that do not take a value can be switched off by inserting a "no" as a prefix to the set parameter. For example, the command

```
:set nonumber
```

switches line numbering off. The command

```
:set
```

shows only the options that you have changed.

The settings that you use in a vi session are (unfortunately) lost each time you exit vi. If you do not like the idea of resetting these options each time you use vi, there is an easier way to perform this initialization. Use the vi initialization file called .exrc. vi searches for this file in your home directory each time it is invoked. If it can't find this file, it uses