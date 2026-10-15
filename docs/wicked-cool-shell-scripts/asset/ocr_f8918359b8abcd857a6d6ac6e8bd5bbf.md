```
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