```
#
# $n is replaced by the logging instance name
# $d is replaced by the current date as Mon-DD-YYYY
# $D is replaced by the current date as YYYYMMDD
# $t is replaced by the starting log time
# $i is replaced by the increment log in the case of multiple logs
# $l is replaced by the log type (dump, status, crypt, etc)
# $h is replaced by the home directory
# ie, "netlogs/$n-$d-$i.dump" called with a logging name of "Pok" could expand
# to something like "netlogs/Pok-Dec-20-01-1.dump" for the first instance and
# "netlogs/Pok-Dec-20-01-2.$1" for the second logfile generated.
# $h/netlogs/$n-$d-$i.dump could expand to
# /home/foo/netlogs/Pok-Dec-20-01-2.dump
#
# Other possibilities: Sorting by directory
# logtemplate=$l/$n-$d-$i
# Would expand to, for example,
# dump/Pok-Dec-20-01-1
# crypt/Pok-Dec-20-01-1
# and so on. The "dump", "crypt", etc, dirs must exist before kismet is run
# in this case.
logtemplate=$n-$d-$i.$l
```

As the comments for the log template say, it looks scary, but it isn't. Using the listed % variables, you can change the order and even the whole filename of the log files. Specifying the `%`/ variable at the beginning will split the log files into separate log files, based on the type of file (dump/ crypt/ and so forth).

The possibilities are endless, so adjust to your needs. The default of logtemplate=%on-%d-%i.%d is replaced with Kismet, %d is replaced with the date, %i is replaced with the log increment, and %l is the file type, in this case it is also used as an extension.

```
# Where do we store the pid file of the server?
piddir=/var/run/
```

The pid file of the server when it's running. There should be no reason to change this unless you are running an odd UNIX variant and need to specify something else.

```
# Where state info, etc, is stored. You shouldn't ever need to change this.
# This is a directory.
confdir=$h/.kismet/
```