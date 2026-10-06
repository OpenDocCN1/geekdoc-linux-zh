# Part I: Getting Started in Fedora RHEL

+   - PATH — The colon-separated list of directories used to find commands that you type.
The default value for regular users is:
- /usr/kerberos/bin:/usr/local/bin:/usr/bin:/bin:/usr/local/sbin:/usr/sbin:/sbin:/home/chris/bin
For the root user, value also includes /sbin, /usr/sbin, and /usr/local/sbin.
- PPID — The process ID of the command that started the shell (for example, its parent process).
- PROMPT_COMMAND — Can be set to a command name that runs each time your shell is displayed. Setting PROMPT_COMMAND=date lists the current date and time before the prompt appears.
- PS1 — Sets the value of your prompt. There are many items that you can read into your prompt (date, time, user name, hostname, and so on). Sometimes a command requires additional prompts, which you can set with the variables PS2, PS3, and so on.(Setting your prompt is described later in this chapter).
- PWD — The directory that is assigned as your current directory. This value changes each time you change directories using the cd command.
- RANDOM — Accessing this variable causes a random number to be generated. The number is between 0 and 32767.
- SECONDS — The number of seconds since the shell was started.
- SHLV — The number of shell levels associated with the current shell session. When you log in to the shell, SHLV is 1. Each time you start a new bash command (by, example, using su to become a new user, or simply typing bash), this number is incremented.
- TIMOUT — Can be set to a number representing the number of seconds the shell can idle without receiving input. After the number of seconds is reached, the shell exits. This is a security feature that makes it less likely for unattended shells to be accessed by unauthorized people. This must be set in the shell for it to logout the user. You can use it in any terminal session to close the shell after a number of seconds, for example TIMOUT=30
- UID — The user ID assigned to your user name. The user ID number is stored in the /etc/password file.

# Setting your own environment variables

Environment variables provide a handy way of storing bits of information that you use often from the shell. You can create any variables (avoiding those that are already in use) so that you can read in the values of those variables as you use the shell. (The bash man page lists variables already in use.)