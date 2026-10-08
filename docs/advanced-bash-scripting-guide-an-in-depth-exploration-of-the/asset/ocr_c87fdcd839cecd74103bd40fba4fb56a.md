# Advanced Bash-Scripting Guide

```
#!/bin/bash
# pid-identifier.sh
# Gives complete path name to process associated with pid.

ARGNO=1 # Number of arguments the script expects.
E_WRONGARGS=66
E_BADPID=66
E_NOSUCHPROCESS=67
E_NOPERMISSION=68
PROCFILE=exe

if [ $1 -ne $ARGNO ];
then
    echo "Usage: $(basename $0) PID-number" >&2 # Error message to stderr.
    exit $E_WRONGARGS
fi

npid=$(ps ax | grep $1 | awk '{ print $1 }' | grep $1)
# Checks for pid in "ps" listing, field #1.
# Then makes sure it is the actual process, not the process invoked by this script.
# The last "grep $1" filters out this possibility.

# # npid=$(ps ax | awk '{ print $1 }' | grep $1)
# also works, as Teemu Huovila, points out.

if [ -z "$npid" ];
then
    # # after all filtering, the result is a zero-length string,
    echo "No such process running."
    exit $E_NOSUCHPROCESS
fi

# Alternatively:
if ! ps $1 >/dev/null 2>&1; 
then
    # # no running process corresponds to the given pid.
    echo "No such process running."
    exit $E_NOSUCHPROCESS
fi

# To simplify the entire process, use "pidof".

if [ ! -r /proc/$1/$PROCFILE ]; 
    # # Check for read permission.
then
    echo "Can't get read permission on /proc/$1/$PROCFILE"
    exit $E_NOPERMISSION # Ordinary user can't access files in /proc.
fi

# The last two tests may be replaced:
if kill -0 $1 >/dev/null 2>&1; # # '0' is not a signal,
    # # this will test whether it is possible
    # # to send a signal to the process.
else
    echo "PID doesn't exist or you're not its owner" >&2
    exit $E_BADPID
fi

_file=$(ls -l /proc/$1 | grep "exe" | awk '{ print $11 }')
# Or exe_file=$(ls -l /proc/$1/exe | awk '{print $11)}')

# # /proc/pid-number/exe is a symbolic link
```

Chapter 29. dev and /proc 466