
Compare this output to that of Red Hat Linux:

```
RHL $ ps
    PID TTY          TIME CMD
    8065 pts/4    00:00:00 bash
    12619 pts/4    00:00:00 ps
```

And finally, compare to the output of OS X:

```
OSX $ ps
    PID TTY          TIME CMD
    37055 ttys000    0:00.01 -bash
    26881 ttys001    0:00.08 -bash
```

Worse, rather than model its ps command after a typical Unix command, the GNU ps command accepts BSD-style flags, SYSV-style flags, and GNU-style flags. A complete mishmash!

Fortunately, some of these inconsistencies can be sidestepped in this particular script by using the -u flag, which produces far more consistent output that includes the owner of the process, the full command name, and—what we're really interested in—the process ID.

This is also the first script where we're really using all the power of the getopts command, which lets us work with lots of different command-line options and even pull in optional values. The script in Listing 6-6 has four starting flags, three of which have required arguments: -s SIGNAL, -u USER, -t TTY, and -n. You'll see them in the first block of code.

## The Code

```
#!/bin/bash

# killall--Sends the specified signal to all processes that match a
# specific process name

# By default it kills only processes owned by the same user, unless you're
# root. Use -s SIGNAL to specify a signal to send to the process, -u USER
# to specify the user, -t TTY to specify a tty, and -n to only report what
# should be done, rather than doing it.

signal="-INT"    # Default signal is an interrupt.
user="" tty="" donothing=0

while getopts "s:u:t:n" opt; do
    case "$opt" in
        # Note the trick below: the actual kill command wants -SIGNAL
        # but we want SIGNAL, so we'll just prepend the "-" below.
        s ) signal="-$OPTARG" ;;
        u ) if [ -z "$tty" ] ; then
            # Logic error: you can't specify a user and a TTY device
            echo "$0: error: -u and -t are mutually exclusive." >&2
            exit 1
        fi
user=$OPTARG;
;;
t ) if [ ! -z "$user" ] ; then
echo "$0: error: -u and -t are mutually exclusive." >&2
exit 1
fi
tty=$2;
;;
n ) donothing=1;
;;
? ) echo "Usage: $0 [-s signal] [-u user|-t tty] [-n] pattern" >&2
exit 1
esac
done

# Done with processing all the starting flags with getopts...
shift $(($OPTIND - 1))

# If the user doesn't specify any starting arguments (earlier test is for -?)
if [ $# -eq 0 ] ; then
echo "Usage: $0 [-s signal] [-u user|-t tty] [-n] pattern" >&2
exit 1
fi

# Now we need to generate a list of matching process IDs, either based on
# the specified TTY device, the specified user, or the current user.

if [ ! -z "$tty" ] ; then
pids=$(ps cu -t $tty | awk "/ $1/ { print $2 }")
elif [ ! -z "$user" ] ; then
pids=$(ps cu -U $user | awk "/ $1/ { print $2 }")
else
pids=$(ps cu -U $(USER:-LOGNAME) | awk "/ $1/ { print $2 }")
fi

# No matches? That was easy!
if [ -z "$pids" ] ; then
echo "$0: no processes match pattern $1" >&2
exit 1
fi

for pid in $pids
do
# Sending signal $signal to process id $pid: kill might still complain
# if the process has finished, the user doesn't have permission to kill
# the specific process, etc., but that's okay. Our job, at least, is done.
if [ $donothing -eq 1 ] ; then
echo "kill $signal $pid"  # The -n flag: "show me, but don't do it"
else
kill $signal $pid
fi
done

exit 0
```

## How It Works

Because this script is so aggressive and potentially dangerous, we’ve put extra effort into minimizing false pattern matches so that a pattern like sh won’t match output from ps that contains bash or vi crashtest.c or other values that embed the pattern. This is done by the pattern-match prefix on the awk command (1, 2, 3).

Left-rooting the specified pattern, $1, with a leading space and right-rooting the pattern with a trailing $ causes the script to search for the specified pattern 'sh' in ps output as ' sh$'.

## Running the Script

This script has a variety of starting flags that let you modify its behavior. The -s SIGNAL flag allows you to specify a signal other than the default interrupt signal, SIGINT, to send to the matching process or processes. The -u USER and -t TTY flags are useful primarily to the root user in killing all processes associated with a specified user or TTY device, respectively. And the -n flag gives you the option of having the script report what it would do without actually sending any signals. Finally, a process name pattern must be specified.

## The Results

To kill all the csmount processes on OS X, you can now use the killall script, as Listing 6-7 shows.

```
$ ./killall -n csmount
kill -INT 1292
kill -INT 1296
kill -INT 1306
kill -INT 1310
kill -INT 1318
```

Listing 6-7: Running the killall script on any csmount processes

## Hacking the Script

There’s an unlikely, though not impossible, bug that could surface while running this script. To match only the specified pattern, the awk invocation outputs the process IDs of processes that match the pattern, plus a leading space that occurs at the end of the input line. But it’s theoretically possible to have two processes running—say, one called bash and the other emulate bash. If killall is invoked with bash as the pattern, both of these processes will be matched, although only the former is a true match. Solving this to give consistent cross-platform results would prove quite tricky.
