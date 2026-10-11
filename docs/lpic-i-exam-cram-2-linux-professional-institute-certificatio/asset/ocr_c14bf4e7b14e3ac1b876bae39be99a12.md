# # Configuring Prompts

Four possible prompts exist on a Linux system, PS1 through PS4. A user usually sees only the PS1 (# or $) prompt, and if he commits a typo or an error in syntax, he might be confronted with the continuation or PS2 (>) prompt.

On a Red Hat machine, the setting for the PS1 prompt is defined in the /etc/bashrc file. In Debian it’s defined in both the /etc/bashrc and the /etc/profile. It’s good to have a backup, is all I can say!

The PS1 variable constitutes the user’s prompt, which is shown every time the user logs in. The PS2 variable normally shows only when lines are continued, such as suffixing a command line with a backslash (\) or if a bracket, parentheses, or quote is left off a command. PS3 and PS4 are rarely used and might as well not exist for the exam’s sake. Table 2.4 lists the special characters for the prompt.

| Table 2.4 | Special Characters for the Prompt |
| :--- | :--- |
| Code | Will Display |
| \a | An ASCII bell character (\07). |
| \d | The date in weekday, month, day format (for example, Tue May 26). |
| \e | An ASCII escape character (\033). |
| \h | The hostname up to the first .. |
| \H | The hostname. |
| \j | The number of jobs currently managed by the shell. |
| \l | The base name of the shell’s terminal device name. |
| \n | New line. |
| \r | Carriage return. |
| \s | The name of the shell. |
| \t | The current time in 24-hour HH:MM:SS format. |
| \T | The current time in 12-hour HH:MM:SS format. |
| \@ | The current time in 12-hour a.m./p.m. format. |
| \A | The current time in 24-hour HH:MM format. |
| \u | The username of the current user. |
| \v | The version of bash (for example, 2.00). |
| \V | The release of bash, in the format version + patch level (for example, 2.00.0). |
| \w | The current working directory. |
| \W | The base name of the current working directory. |