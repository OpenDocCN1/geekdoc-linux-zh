# Table 13.3 Job Control Commands (continued)

| Command | Meaning |
|---|---|
| stty tostop | Suspends a background job if it sends output to the terminal |
| wait [n] | Waits for a specified job and returns its exit status; n is a PID or job number |
| ^Z (Ctrl-Z) | Stops (suspends) the job; the prompt appears on the screen |
| Argument to Jobs Command | Represents |
| %n | Job number n |
| %string | Job name starting with string |
| %string | Job name containing string |
| %% | Current job |
| %+ | Current job |
| %- | Previous job, before current job |
| -r | Lists all running jobs |
| -s | Lists all suspended jobs |

New jobs Options. Two new options were added to the jobs command in bash versions 2.x. They are the -r and -s options. The -r option lists all running jobs, and the -s option lists all stopped jobs.

The disown Built-In. The disown built-in command (bash 2.x) removes a specified job from the job table. After the job has been removed, the shell will no longer recognize it as a viable job process and it can only be referenced by its process ID number.

# 13.5 Command-Line Shortcuts

# 13.5.1 Command and Filename Completion

To save typing, bash implements command and filename completion, a mechanism that allows you to type part of a command or filename, press the Tab key, and the rest of the word will be completed for you.

If you type the first letters in a command and press the Tab key, bash will attempt to complete the command and execute it. If bash cannot complete the filename or command, because neither exists, the terminal may beep and the cursor will stay at the end of the command. If there is more than one command starting with those characters and you press the Tab key a second time, all commands that start with those characters will be listed.