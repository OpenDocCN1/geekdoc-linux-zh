# ## whatis

**Purpose:** Display a description of the specified command.

**Usage syntax:** `whatis [OPTIONS] [COMMAND]`

```
$ whatis ls
ls (1) - list directory contents
```

Viewing the manual description of the ls command

`whatis` displays a brief description of the specified command. The above example displays the description of the `ls` command using `whatis`. This can be used as a helpful reminder of a command's purpose without having to refer to the `man` command.

Multiple commands can be used with one `whatis` query to display the description of each individual command. For example, typing `whatis ls who rm` would display the description of all three commands at once as demonstrated in the next example.

```
$ whatis ls who rm
ls (1) - list directory contents
who (1) - show who is logged on
rm (1) - remove files or directories
```

Viewing the manual description of multiple commands

> > **Note**
> > *Some Unix systems may use the apropos command in place of whatis.*

+   Common usage examples:
+   
+   - `whatis [COMMAND]` - Display the description of the specified command
+   - `whatis -w [WILDCARD]` - Search for commands using a wildcard