11.08.2015.14:34
$

The date specified is *month.day.year.hour:minute.*

# 2. Now I create a snapshot filename with this suffix:

Click here to view code image

```
snapdir="$HOME/Snapshots"
thedate="$(date +%m.%d.%Y.%H:%M)"
outfile="$snapdir/snapshot.$thedate.tar.gz"
```

This saves the date/time format as variable `thedate` and then creates an `outfile` filename for use later in the script that is prefaced with the name of the snapshot directory. On my system, `outfile` ends up looking like this:

Click here to view code image

```
/home/taylor/Snapshots/snapshot.12.08.2015.14:40.tar.gz
```

This is just what I want.

# 3. There isn’t much more to the script—just the actual invocation to the `tar` command itself. To make it a bit more sophisticated, the script will use the first argument, if present, as the directory to back up. Otherwise, it’ll use the current directory as the default. Also notice the use of the `-z` flag to automatically `zip` the resultant output (which is why the `.gz` was added to the `outfile` variable above, too).

Here’s the entire script, short and sweet:

Click here to view code image

```
$ cat snapshot.sh
#!/bin/bash

snapdir="$HOME/Snapshots"
thedate="$(date +%m.%d.%Y.%H:%M)"
outfile="$snapdir/snapshot.$thedate.tar.gz"

if [ $# -gt 0 ] ; then
  dirs=$1
else
  dirs="."
fi

echo "Backing up $dirs to $outfile"

tar -czf $outfile $dirs

echo "done."

exit 0
$
```

# 4. And here it is in use:

Click here to view code image

```
$ alias snapshot="$HOME/bin/snapshot.sh"
$ snapshot
Backing up . to /home/taylor/Snapshots/snapshot.11.08.2015.14:50.tar
```