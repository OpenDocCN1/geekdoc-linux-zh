```
# xfs_repair -1 /dev/sdc1 -n
```

+   5. What is the difference between the -T and -t parameters for df?

The parameter -T will include the type of each filesystem in the output of df. -t is a filter, and will show only filesystems of the given type on the output, excluding all others.