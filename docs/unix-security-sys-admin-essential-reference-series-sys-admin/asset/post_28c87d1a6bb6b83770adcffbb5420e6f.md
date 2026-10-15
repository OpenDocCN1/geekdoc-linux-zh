
The directories named after the init levels represent the usual way UNIX SVR4 handles the run commands. The filenames in those directories begin with an S or a K to identify scripts that start or kill processes. A two-digit sequence number that follows the S or K identifies which file in the S or K group must run first. The rest of the filename generally identifies what the script does. For example, Table 4.1 shows a sample rc2.d directory's contents, and Table 4.2 shows a sample rc0.d directory's contents.

Another method for handling the run commands uses the rc.d directory. The rc.d directory contains subdirectories named with single digits from 0 to 9, representing the execution sequence of all scripts found in those directories. Put a script in that directory to execute it during system startup or shutdown.

Figure out which method your system uses and change either /etc/rc.d/8/userdef or /etc/rc2.d/S88USERDEFINE to start idleout with the number of minutes you want to allow.

## killidle Script

If you don't have SCO UNIX, you can still kill idle tty processes with a shell script. The script combines who(1) and awk(1). The who command identifies the ttys in use and their idle times. The awk script analyzes who's output, decides which ttys are too old, and puts them out of our misery. Listing 4.1 shows the killidle script.

The colon in the first line forces a Bourne shell to execute the script. The first code line,

```
IDLEOUT=$1:-20
```

sets the IDLEOUT variable to either the value in killidle's first command line argument or 20. Instead of using if tests to see whether there is a $1 argument, I use the shell's own variable substitution mechanism. (See the sidebar "Shell Variable Substitution" for more information on this mechanism.) This syntax says that if $1 has a value, use it. If there is no $1 or it has a 0 value, use the 20. Whichever is selected, assign the result to the variable IDLEOUT.

The next step avoids trouble if the user gives a negative time. I chose to set IDLEOUT to the default 20 minutes if a negative time is discovered. As another approach, you might use expr to change the value's sign.

With IDLEOUT valid, the script uses the who command to get the user list. The -u option limits the output to only those people currently in. It also shows the idle time for each of those logins. The code pipes the output to the awk program to process that idle time.

The awk script doesn't contain a pattern, just an action. To keep things easy, it extracts the column values needed for analysis and output: the user's name, the terminal ID, the idle time, and the login's Process ID (PID).

If a user has pressed a key at the tty within the last minute, that tty's idle column shows a period. The script's first if test eliminates that condition from the script's concern. Given some idle time amount, who shows it in the format hours:minutes. The hours may be set to 0. Only the minutes are needed for this script.

## Shell Variable Substitution

You can test and change the shell variables in a variety of ways without using the shell's if command or the test(1) command. I show only the Bourne shell's methods here, because it is the shell used most portably for programming. However, csh's and ksh's substitution abilities are richer than sh's abilities. If you're programming with either of the other shells, spend time investigating their substitution features. They're worth it. $n surrounds the variable name with braces, putting the $ outside of the braces, when referring to a variable substitution operation.

${var} Use this format when embedding the value of a variable inside another value, such as a prefix or suffix. If the other value won't confuse the shell about the name of the variable, you don't need the braces. For example, given

```
things=more
want=${things}stuff
```

the variable $want gets the value morestuff. Without the braces, the shell might think the variable name is $thingsstuff. However, in the directory setting

```
newdir=$SMANDIR/new
```

the braces aren't needed because the slash is a sufficient separator.

${var:-value} If the variable exists in the environment and has a value, yield its value. Otherwise, use the value named after the :- characters. This is the simplest form of substitution, yielding the named value only if the variable doesn't already have one.

${var:=value} If the variable exists in the environment and has a value, yield its value. Otherwise, assign the value named after the := characters to the variable and yield the new value.
