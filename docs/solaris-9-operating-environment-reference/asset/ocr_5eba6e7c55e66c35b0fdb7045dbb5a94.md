# 196

# csh

+   1. Reads a line of command input and breaks it into words.
2. Puts the sequence of words in the history list and then parses them.
3. Executes each command in the current line.

# Noninteractive Operation

When running noninteractively, the shell does not prompt for input from the terminal. A noninteractive C shell can execute a command as an argument on its command line or can interpret commands from a file, also known as a script.

> Note — When the shell executes a shell script that attempts to execute a nonexistent command interpreter, the shell returns an erroneous diagnostic message that the shell script file does not exist.

# Options

+   -b Force a “break” from option processing. Do not interpret subsequent command-line arguments as C shell options. This enables the passing of options to a script without confusion. You must use this option or the shell will not run setuid or setgid scripts.
-c Execute the first argument (which must be present). Remaining arguments are placed in argv, the argument-list variable, and passed directly to csh.
-e If a command terminates abnormally or yields a non-zero exit status.
-f For a fast start, read neither the .cshrc file nor the .login file (if a login shell) on startup.
-i Force interactive mode. Prompt for command-line input, even if the standard input does not appear to be a terminal (character special device).
-n Parse (interpret), but do not execute commands. You can use this option to check C shell scripts for syntax errors.
-s Take commands from the standard input.
-t Read and execute a single command line. You can use a backslash (\) to escape each newline for continuation of the command line onto subsequent lines.
-v Set the verbose predefined variable; echo command input after history substitution (but before other substitutions) and before execution.
-V Set verbose before reading .cshrc.
-X Set the echo variable. Echo commands after all substitutions and just before execution.
-X Set echo before reading .cshrc.

With the options -c, -i, -s, or -t, take the first non-option argument to be the name of a command or script. Pass it as argument zero, and add subsequent arguments to the argument list for that command or script.