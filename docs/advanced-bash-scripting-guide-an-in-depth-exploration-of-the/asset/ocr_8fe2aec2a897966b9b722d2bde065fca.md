# Advanced Bash-Scripting Guide

```
if [ ! -e /proc/$pidno/$PROCFILENAME ]
# While process running, then "status" file exists.
then
echo "Disconnected."
# exit $NOTCONNECTED
fi

netstat -s | grep "packets received" # Get some connect statistics.
netstat -s | grep "packets delivered"

sleep $INTERVAL
echo:

done
exit 0
```

# As it stands, this script must be terminated with a Control-C

+   - Exercises:
  ------
- Improve the script so it exits on a "q" keystroke.
- Make the script more user-friendly in other ways.
- Fix the script to work with wireless/DSL connections.

> In general, it is dangerous to write to the files in /proc, as this can corrupt the filesystem or crash the machine.