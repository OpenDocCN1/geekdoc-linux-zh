# Chapter I: SETTING UP 29

e) What happens to the process ID if you run this command again?

# 1.3.2 “DOT” A SCRIPT

The second way to run a script is to "dot" it. That is, you type a dot ( . ), followed by a space and the name of the script (or function) that you want to run. When you run a script this way, it uses the shell's environment instead of having its own.

Run the following pair of commands to see the implications of dotting a script compared with running it as a command. You should not have changed s131 or VAR_131 since the previous exercise.

```
print $$
s131
```

+   a) What is the process ID of your interactive shell?

+   b) What is the script's process ID when you dot it?

Now add the following commands to the end of ~/bin/s131:

```
VAR_131=changed
print "Now VAR_131 is \\$VAR_131\"
```

Now you can see another of the shell's features. called subshells. You can run the command(s) in a subshell by putting parentheses around it (or them). To