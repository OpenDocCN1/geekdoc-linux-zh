# OPTIONS (CONT.)

| Use This Option | To Do This |
|---|---|
| -t type | Load only those modules of the specified type |
| -c | Display the current module configuration |
| -I | List currently available modules |
| -v | Show all messages |
| -V | Display version information |
| -a | Load all modules until one is found that works |

# EXAMPLES

| This Command | Does the Following |
|---|---|
| modprobe -c | Shows the current module configuration. |
| modprobe -a -t sound | Attempts to load all the modules of the type sound until one is found that works. |
| modprobe aha152x aha152x='0x340,12,7,5' | Loads the module named aha152x and sets the option (aha152x) to the specified values ('0x340,12,7,5'). |

# passwd

``passwd [ option ] username``
Enables the user specified by *username* to change the password currently assigned to the account. A user with root privileges may use this command to change any user's password.

# OPTIONS

| Use This Option | To Do This |
|---|---|
| -k | Update the expired passwords only. |
| -l | Lock this account and make it accessible to the root user only. Requires root user status. |