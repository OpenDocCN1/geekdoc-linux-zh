
default_duration=7    # We'll default to a 7-day rotation schedule.
count=0

duration=$default_duration

if [ ! -f $config ] ; then
# No config file for this script? We're out. You could also safely remove
# this test and simply ignore customizations when the config file is
# missing.
echo "50: no config file found. Can't proceed." >&2
exit 1
fi

if [ ! -w $logdir -o ! -x $logdir ] ; then
# -w is write permission and -x is execute. You need both to create new
# files in a Unix or Linux directory. If you don't have 'em, we fail.
echo "50: you don't have the appropriate permissions in $logdir" >&2
exit 1
fi

cd $logdir

# While we'd like to use a standardized set notation like :digit: with
# the find, many versions of find don't support POSIX character class
# identifiers-hence [0-9].

# This is a pretty gnarly find statement that's explained in the prose
# further in this section. Keep reading if you're curious!

for name in $(find . -maxdepth 1 -type f -size +0c ! -name "*[0-9]*" \
! -name "\.*" ! -name "*conf" -print | sed 's/^\.\///')
do

count=$(($count + 1))
# Grab the matching entry from the config file for this particular log file.
duration="$(grep "^${name}" $config|cut -d' ' -f2)"

if [ -z "$duration" ] ; then
duration=$default_duration  # If there isn't a match, use the default.
elif [ "$duration" = "0" ] ; then
echo "Duration set to zero: skipping $name"
continue
fi

# Set up the rotation filenames. Easy enough:

back1="${name}.1"; back2="${name}.2";
back3="${name}.3"; back4="${name}.4";

# If the most recently rolled log file (back1) has been modified within
# the specific quantum, then it's not time to rotate it. This can be
# found with the -mtime modification time test to find.

if [ -f "$back1" ] ; then
if [ -z "$(find \'$back1\' -mtime +$duration -print 2>/dev/null)" ]
then
/bin/echo -n "$name's most recent backup is more recent than $duration "
echo "days: skipping" ;  continue
fi
fi
echo "Rotating log $name (using a $duration day schedule)"
# Rotate, starting with the oldest log, but be careful in case one
#  or more files simply don't exist yet.
if [ -f "$back3" ] ; then
echo "... $back3 -> $back4" ; $mv -f "$back3" "$back4"
fi
if [ -f "$back2" ] ; then
echo "... $back2 -> $back3" ; $mv -f "$back2" "$back3"
fi
if [ -f "$back1" ] ; then
echo "... $back1 -> $back2" ; $mv -f "$back1" "$back2"
fi
if [ -f "$name" ] ; then
echo "... $name -> $back1" ; $mv -f "$name" "$back1"
fi
touch "$name"
chmod 0600 "$name"  # Last step: Change file to rw------ for privacy
done
if [ $count -eq 0 ] ; then
echo "Nothing to do: no log files big enough or old enough to rotate"
fi
exit 0

## Listing 6-12: The rotatelogs script

To be maximally useful, the script works with a configuration file that lives in /var/log, allowing the administrator to specify different rotation schedules for different log files. The contents of a typical configuration file are shown in Listing 6-13.

```
# Configuration file for the log rotation script: Format is name=duration,
#  where name can be any filename that appears in the /var/log directory.
# Duration is measured in days.

ftp.log=30
lastlog=14
lookupd.log=7
lpr.log=30
mail.log=7
```

```
netinfo.log=7
secure.log=7
statistics=7
system.log=14
# Anything with a duration of zero is not rotated.
wtmp=0
```

Listing 6-13: An example configuration file for the rotatelogs script

## How It Works

The heart of this script, and certainly the most gnarly part, is the find statement at 1. The find statement creates a loop, returning all files in the /var/log directory that are greater than zero characters in size, don't contain a number in their name, don't start with a period (OS X in particular dumps a lot of oddly named log files in this directory—they all need to be skipped), and don't end with conf (we don't want to rotate out the rotatelogs.conf file, for obvious reasons). maxdepth 1 ensures that find doesn't step into subdirectories, and the sed invocation at the very end removes any leading ./ sequences from the matches.

> NOTE
> Lazy is good! The rotatelogs script demonstrates a fundamental concept in shell script programming: the value of avoiding duplicate work. Rather than have each log analysis script rotate logs, a single log rotation script centralizes the task and makes modifications easy.

## Running the Script

This script doesn't accept any arguments, but it does print messages on which logs are being rotated and why. It should also be run as root.

## The Results

The rotatelogs script is simple to use, as shown in Listing 6-14, but beware that depending on file permissions, it might need to be run as root.

```
$ sudo rotatelogs
ftp.log's most recent backup is more recent than 30 days: skipping
Rotating log lastlog (using a 14 day schedule)
... lastlog -> lastlog.1
lpr.log's most recent backup is more recent than 30 days: skipping
```

Listing 6-14: Running the rotatelogs script as root to rotate the logs in /var/log

Notice that only three log files matched the specified find criteria in this invocation. Of these, only lastlog hadn't been backed up sufficiently recently, according to the duration values in the configuration file. Run rotatelogs again, however, and nothing's done, as Listing 6-15 shows.
