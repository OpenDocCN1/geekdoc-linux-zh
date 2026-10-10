# whatis

**Purpose**: Display a description of the specified command.

**Usage syntax**: `whatis [OPTIONS] [COMMAND]`

![](bbox=[0.14, 0.17, 0.86, 0.23])

**whatis** displays a brief description of the specified command. The above example displays the description of the **ls** command using **whatis**. This can be used as a helpful reminder of a command's purpose without having to refer to the **man** command.

Multiple commands can be used with one **whatis** query to display the description of each individual command. For example, typing **whatis ls who rm** would display the description of all three commands at once as demonstrated in the next example.

![](bbox=[0.14, 0.47, 0.86, 0.54])

> Some Unix systems may use the apropos command in place of whatis.

**Common usage examples:**

| `whatis [COMMAND]` | Display the description of the specified command |
| `whatis -w [WILDCARD]` | Search for commands using a wildcard |