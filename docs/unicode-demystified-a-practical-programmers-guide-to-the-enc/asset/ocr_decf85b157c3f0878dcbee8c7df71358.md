To see a list of the current aliases, give the command alias. To view the aliases for a particular name, give the command alias followed by the name.

# Differences between the tsh and bash Mechanisms

The alias builtin and substitution used in bash are patterned after the alias builtin found in the Z Shell. It is slightly different from the alias builtin used in tsh, which is patterned after the alias builtin found in the TC Shell. The syntax of the version used by tsh

alias name value

The tsh version of alias (next section) lets you to substitute the command arguments. To do something similar in bash, you have to use a shell function (672).

# History Substitution in an Alias

You can substitute command line arguments by using the history mechanism, with a single exclamation point representing the input line containing the aliases. Modifiers are the same as those used by history (page 686). The exclamation points are quoted in the following example so that the shell does not interpret them when building the aliases (which would produce incorrect results):

+   - 21% alias last echo !$
- 22% last this is just a test
- 23% alias fn2 echo :2:t
- 24% fn2 /home/jenny/test /home/alex/temp /home/barbara/new
temp

Event 21 defines for an alias that displays the last argument. Event 23 defines for fn2 an alias that displays the simple filename, or tail, of the second argument on the command line.

# Job Control

Job control in bash (page 554) and in tsh is similar. You can move commands between the foreground and background, suspend jobs temporarily, and get a list of the current jobs. The % character references a job when followed by a job number or a string prefix that uniquely identifies the job. You will see a minor difference when you run a multiple-process command line in the background. Bash displays only the PID of the last background process in each job, tsh displays the numbers for all the processes belonging to a job. The example from page 554 looks like this:

```
tsh $ find -print | sort | lpr & grep -1 alex /tmp/ * > alexfiles & &
[1] 18839 18840 18841
[2] 18876
```