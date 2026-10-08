# Advanced Bash-Scripting Guide

+   • Quote a variable containing whitespace prevents splitting. Sometimes this produces unintended.

Commands from a script may fail to execute because the script owner lacks permission for them. If a user cannot invoke a command from the command-line, then piping it into a script will likewise fail. Try changing the attributes of the command in question, perhaps even setting the suid bit (as root,) of root.

Attempting to use 2> | command2 (not) will result in an unpleasant surprise.

```
command1 2> | command2
# Trying to redirect error output of command1 into a pipe . . .
# . . will not work.

command1 2& | command2 # Also futile.
```

Thanks, S.C.

Using Bash version 2+ functionality may cause a bailout with error messages. Older Linux machines have version 1.XX as the default installation.

```
#!/bin/bash

minimum_version=2
# Since Chet Rainy is constantly adding features to Bash,
# you may set $minimum_version to 2.XX, 3.XX, or whatever is appropriate.
E_BAD_VERSION=8
```

```
if [ "$BASH_VERSION" -lt "$minimum_version" ]
then
    echo "This script works only with Bash, version $minimum or greater.
    echo "Upgrade strongly recommended."
    exit $E_BAD_VERSION
fi
```

+   • Using Bash-specific functionality in a Bourne shell (#/bin/sh) on a non-Linux machine may cause unexpected behavior. Linux system usually aliases sh to bash, but this does not necessarily hold true for generic UNIX maths.

Using undocumented features in Bash turns out to be a dangerous practice. In previous releases of this book there were several scripts that depended the maximum value of an exit or return value was 25, which did not apply to negative integers. Unfortunately, in version 2.05b and later, that loophole disappeared. See 24-9.

+   • In some contexts, a misleading state may be returned. when setting a local variable within a function or assigning an arithmetic value to a variable.

+   • The exit of an arithmetic expression is not equivalent to an error code.

```
var=1 && ((--var)) && echo $var
    # Here the and-list terminates with exit status 1.
echo $? # 1
    $var doesn't echo!
```

34. Gotchas

493