points.

+   - **-m** Report message and semaphore activities:

msg/s Number of System V msgrcv() calls per second;

sema/s Number of System V semop() calls per second;

select/s Number of System V select() calls per second. This value will only be reported if the "-S" option is also explicitly specified.

- **-A** Report all data. Equivalent to -udgbwcayvm.

- **-M** Report the per-processor data on a multi-processor system when used with -q and/or -u options. If the -M option is not used on a multi-processor system, the output format of the -u and -q options is the same as the uni-processor output format and the data reported is the average value of all the processors.

# EXAMPLES

Watch CPU activity evolve for 5 seconds:

sar 1 5

Watch CPU activity evolve for 10 minutes and save data:

sar -o temp 60 10

Review disk and tape activity from that period later:

sar -d -f temp

Review cpu utilization on a multi-processor system later:

sar -u -M -f temp

# WARNINGS

Users of sar must not rely on the exact field widths and spacing of its output, as these will vary depending on the system, the release of HP-UX, and the data to be displayed.

# FILES

+   * `/var/adm/sa/sadd` daily data file, where dd is two digits representing the day of the month.

# SEE ALSO

sal(1M).

# STANDARDS CONFORMANCE

sar: SVID2, SVID3