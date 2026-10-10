# **OPTIONS**

| Use This Option | To Do This |
| :--- | :--- |
| -I, --list-shells | Display a list of available shells |
| -s shell, --=shell shell | Switch to the specified shell |
| -u, --help | Display available options |
| -v, --version | Show the version number |

# **declare**

declare [options ] [ name [= value] ]
Displays or changes variables. When used without options or arguments, prints a list of all the currently assigned variables and their values. To create or reset a variable, specify the name and value.

# **OPTIONS**

| Use This Option | To Do This |
| :--- | :--- |
| -f | Show function names only |
| -r | Create variable as read-only |
| -x | Mark variables for export |
| -1 | Restrict value to integers |

# **EXAMPLES**

| This Command | Does the Following |
| :--- | :--- |
| declare | Shows the current variables and values. |
| declare docs=' /home/bryan/ Documents' | Creates the specified variable (docs) and assigns the value /home/bryan/Documents. |