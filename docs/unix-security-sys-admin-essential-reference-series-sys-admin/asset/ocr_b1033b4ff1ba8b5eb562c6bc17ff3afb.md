If a user has pressed a key at the tty within the last minute, that tty's idle column shows a period. The script's first if test eliminates that condition from the script's concern. Given some idle time amount, who shows it in the format hours:minutes. The hours may be set to 0. Only the minutes are needed for this script.

# Shell Variable Substitution

You can test and change the shell variables in a variety of ways without using the shell's if command or the test(1) command. I show only the Bourne shell's methods here, because it is the shell used most portably for programming. However, csh's and ksh's substitution abilities are richer than sh's abilities. If you're programming with either of the other shells, spend time investigating their substitution features. They're worth it. $n surrounds the variable name with braces, putting the $ outside of the braces, when referring to a variable substitution operation.

$!var Use this format when embedding the value of a variable inside another value, such as a prefix or suffix. If the other value won't confuse the shell about the name of the variable, you don't need the braces. For example, given

```
things=more
want=${things}stuff
```

the variable $want gets the value morestuff. Without the braces, the shell might think the variable name is $thingsstuff. However, in the directory setting

```
newdir=$SMANDIR/new
```

the braces aren't needed because the slash is a sufficient separator.

$!var:-value If the variable exists in the environment and has a value, yield its value. Otherwise, use the value named after the :- characters. This is the simplest form of substitution, yielding the named value only if the variable doesn't already have one.

$!var:=value If the variable exists in the environment and has a value, yield its value. Otherwise, assign the value named after the := characters to the variable and yield the new value.