# rehash — Evaluate the Internal Hash Table of the Contents of Directories

# Synopsis

csh
rehash

# Description

See hash(1).

# remote_shell, remsh — Remote Shell

# Synopsis

```
remsh [-n] [-i username] hostname command
remsh hostname [-n] [-l username] command hostname [-n] [-l username]
command
```

# Description

See rsh(1).

# renice — Alter Priority of Running Processes

# Synopsis

```
/usr/bin/renice [-n increment] [-i itype] [-u] ID...
usr/bin/renice [-n increment] [-g | -p] [-u] ID... (This syntax is obsolete
starting with the Solaris 9 release.)
/usr/bin/renice priority [-p] pid... [-g gid...] [-p pid...]
[-u user...]
/usr/bin/renice priority -g gid... [-p pid...] [-u user...]
usr/bin/renice priority -u user -g gid...] [-p pid...] [-u user...]
```

# Description

> Note — The proiccntl command subsumes the function of renice.

Use the renice command to adjust the scheduling priority of one or more running
processes. By default, specify the processes to be affected by their IDs.
If the first operand is a number within the valid range of priorities (-20 to 20), renice
treat it as a priority (as in all but the first synopsis form); otherwise, renice treats it
an an ID (as in the first synopsis form).