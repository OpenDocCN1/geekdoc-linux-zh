# Advanced Bash-Scripting Guide

else
echo "You are just a regular fella."
fi
See also Example 2-3.

> The variables $ENV, $LOGNAME, $MAIL, $TERM, $USER, and $USERNAME are not Bash builtins. These are however, often set as environmental variables in one of the Bash or login script files. $SHELL, the name of the user's login file, may be set from /etc/passwd or in an "init" script, and it is likewise not a Bash builtin.

```
tcsh% echo $LOGNAME
bozo
tsh% echo $SHELL
/bin/tcsh
tsh% echo $TERM
rxvt

bash$ echo $LOGNAME
bozo
bash$ echo $SHELL
/bin/tcsh
bash$ echo $TERM
rxvt
```

# Positional Parameters

$0, $1, $2, etc.

Positional parameters, passed from command line to script, passed to a function, or set to a variable (see Example 4-5 and Example 15-16)

$# Number of command-line arguments [44] or positional parameters (see Example 36-2)

$* All of the positional parameters, seen as a single word

> "$+" must be quoted.

$@ Same as $*, but each parameter is a quoted string, that is, the parameters are passed on intact, without interpretation or expression. This means, among other things, that each parameter in the argument list is seen as a separate word.

> Of course, "$@" should be quoted.

# Example 9-6. arglist: Listing arguments with $* and $@

# Chapter 9. Another Look at Variables