# **echo**

echo [ option ] [ string ]
Displays the specified string on the display. This command can also be used to show the values of variables and functions.

# OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| -n | Not add a newline character to the output |
| -e | Enable interpretation of escape characters |
| -E | Disable interpretation of escape characters |

# EXAMPLE

| This Command | Does the Following |
| :--- | :--- |
| echo $USER | Shows the current user's name. |

# **env**

env [ option ] [ variable=value ] [ command ]
This utility displays or sets the specified variable. When you type this command without options or arguments, it displays all the current variables and their values. If you specify a command, the command is executed in the altered environment.

# OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| -u variable, --unset variable | Unset the specified variable |
| -i, --ignore-environment | Ignore the current environment |