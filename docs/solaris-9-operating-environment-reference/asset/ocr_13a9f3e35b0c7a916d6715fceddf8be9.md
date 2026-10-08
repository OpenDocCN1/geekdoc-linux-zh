# 1112

# prioctl

as a real-time process with a real or effective user ID matching the real or effective user
ID of the target process.

The real-time priority, time quantum, and time quantum signal are inherited across other class,
fork(2) and exec(2) system calls. When you use the time quantum signal with a
user-defined signal handler across the exec(2) system call, the new image must install
an appropriate user-defined signal handler before the time quantum expires.
unpredictictable behavior results.

# Timesharing Class

The timesharing policy provides for a fair and effective allocation of the CPU
resource among processes with varying CPU consumption characteristics.
Theobjectives of the timesharing policy are to provide good response time to interactive
processes and good throughput to CPU-bound jobs while providing a degree of user or
application control over scheduling.

The timesharing class has a range of timesharing priority (tspri) values which
be assigned to processes within the class. User priorities range from -xo +x where
the value of x is configurable. You can display the priority for a specific installation with
t prioctl -l

The user priority provides some degree of user or control over the
scheduling of processes in the timesharing class. Raising or lowering the tspri value of
a process in the timesharing class raises or lowers the scheduling priority of the
process. However
value runs before one with a lower tspri value, because the tspri value is just one
factor to determine the scheduling priority of a timesharing process. The system
dynamically adjust the internal scheduling priority of a timesharing process based
on other factors such as recent CPU usage.

In addition to the limits on user priority (displayed with prioctl -1),
a per-process priority limit (tsprilim) specifies the maximum tspri value that
can be set for a given process.

The prioctl -d [idtype] [idlist] command displays the user priority and
tuser priority limit for each process in the set specified by idtype and
idlist.

Any timesharing process can lower its own tspilim(or that of another process
with the same user ID). Only a timesharing process with superuser privilege can
tspilim When changing the class of a process to timesharing from some other
class, you must have superuser privilege to set the tspri to a greater value
b.

Any timesharing process can set its own tspri(or that of another process with
the same user ID) to any value less than or equal to the tspilim Attempts to set
the tspri above the above(and/or the tspilim below the tspri value) sets the
tspri equal to the tspilim.

You can use any combination of the -m and -options with prioctl -s or prioctl
- for timesharing. If you omit an option and the process is currently
timesaring, the associated parameter is normally unaffected. The exception is that you
can omit the p option and use -m to set the current tspri. In this
case, the tspri is equal to the tspilim below being set. If you omit an option
when changing the class of a process to timesharing from some other class,
associated parameter is set to a default value. The default value for tspurilim is 0, and
t default for tspri is to be equal to the tspilim value that is being set.

The timesharing user priority and user priority limit are inherited across the fork(2)
and exec(2) system calls.