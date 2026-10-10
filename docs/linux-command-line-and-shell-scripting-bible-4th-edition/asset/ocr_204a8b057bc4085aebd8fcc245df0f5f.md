```
directory:

    -rw-r--r--    1 user     user        769 Jun 01 16:15
        log.200601
```

The log file appears in the directory using the value of the `$today` variable as part of the filename. The contents of the log file are the directory listing from the /usr/bin directory. If the script is run the next day, the log filename will be log.200602 , thus creating a new file for the new day.

WARNING
Command substitution creates what's called a subshell to run the enclosed command. A subshell is a separate child shell generated from the shell that's running the script. Because of that, any variables that you create in the script won't be available to commands running in the subshell.

Subshells are also created if you run a command from the command prompt using the ./ path, but they aren't created if you just run the command without a path. However, if you use a built-in shell command, that doesn't generate a subshell. Be careful when running scripts from the command prompt!

# Redirecting Input and Output

There are times when you'd like to save the output from a command instead of just having it displayed on the monitor. The Bash shell provides a few different operators that allow you to redirect the output of a command to an alternative location (such as a file). Redirection can be used for input as well as output, redirecting a file to a command for input. This section describes what you need to do to use redirection in your shell scripts.

# Output redirection