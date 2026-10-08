# 618

# ksh, rksh

can be a number in the unit specified below with each resource, or the value unlimited. The Hand options specify whether the hard limit or the soft limit for the given resource is set. Once a hard limit is set, you cannot increase it. You can increase a soft limit up to the value of the hard limit. If you specify neither h nor s option, the limit applies to both. Print the current resource limit when you omit limit. In this case, the soft limit unless unless you specified it. When you specify more than one resource, print the limit name and before the value.

List all of the current resource limits.

+   -a The number of 512-byte blocks on the size of core dumps.

+   -c The number of kilobytes on the size of the data area.

+   -d The number of 512-byte blocks on files written by children processes (files of any size may be read).

+   -n The number of file descriptors plus 1.

+   -s The number of kilobytes on the size of the stack area.

+   -t The number of seconds to be used by each process.

+   -v The number of kilobytes for virtual memory. If you specify no option, assume -f.

```
umask [-S] [mask]
```

Set the user-creation mask to (see umask(2)). mask can be either an octal or a symbolic value as described in chmod(1). If you specify a symbolic value, the new umask is the complement of the result of applying mask to the complement of the previous umask value. If you omit mask, print the current value of the mask. The -S option produces symbolic output.

unalias name...

Remove the aliases given by the list of names from the alias list.

unset [-f] name...

Unassign the variables given by the list of names, that is, erase their values and attributes. You cannot unset read-only variables. If you specify -f option, the names refer to function names. Unsetting ERRNO, LINENO, MAILCHECK, OPTARG, OPTIND, RANDOM, SECONDS, MOUT, and _ removes their special meaning even if they are subsequently assigned.

+   * wait [job]

Wait for the specified job, and report its termination status. If you do not specify job wait for all currently child processes. The exit status from this command is that of the process waited. See "Job Control" on page 586 for a description of the format of job

![](bbox=[0.181, 0.955, 0.235, 0.972])