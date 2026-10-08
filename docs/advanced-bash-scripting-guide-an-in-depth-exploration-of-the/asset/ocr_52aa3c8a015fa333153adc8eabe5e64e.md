# Advanced Bash-Scripting Guide

```
TIME_LIMIT=10
INTERVAL=1

echo
echo "Hit Control-C to exit before $TIME_LIMIT seconds."
echo

while [ "$SECONDS" -le "$TIME_LIMIT" ];
  # $SECONDS is an internal shell variable.
  if [ "$SECONDS" -eq 1 ];
  then
    units=second
  else
    units=seconds
  fi

echo "This script has been running $SECONDS $units."
  # On a slow or overloaded machine, the script may skip a count
  +# every once in a while.
  sleep $INTERVAL
done
echo -e "\a" # Beep!

exit 0
```

$SHELLOPTSnThe list of enabled options, a readable variable.

```
bash echo $SHELLOPTS
braceexpand:hashall:histext:monitor:history:interactive-comments:emacs
```

$SSHLLV
Shell level, how deeply Bash is nested. [43] If, at the command-line, $SSHLLV is 1, in a script it
will increment to 2.

> This variable is not affected by subshells. Use $BASH SUBSHELL, when you need
an indication of shell nesting.

$MOUT
The $MOUT environmental variable is set to a non-zero value time, then the shell prompt will
time out after $shell seconds. This will cause a logout.

As of 2.05b of Bash, it is now possible to use $MOUT in a script in combination with read.

```
# Works in scripts for Bash, 2.05b and later.
TMOUT=3    # Prompt times out at three seconds.
echo "What is your favorite song?"
echo "Quickly now, you have only $TMOUT seconds to answer!"
read read song

if [ -z "$song" ];
then
  song="(no answer)"
  # Default response.
fi
```

Chapter 9. Another Look at Variables