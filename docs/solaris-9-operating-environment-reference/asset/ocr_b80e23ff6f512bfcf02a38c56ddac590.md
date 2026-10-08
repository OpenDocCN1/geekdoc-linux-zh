# 1202

# sar

be difficult to read. (If the sampling interval is less than 5, the activity of sar itself
afect the sample.) If you specify the -o option, sar saves the samples in filename
binary format. The default value of n is 1.

In the second synopsis format, you specify no sampling interval. Instead, sar extracts
data from a previously recorded file name, either the one specified by the -f option or,
by default, the standard-system-activity data file /var/adm/sa/sad for the current
day You can bound the starting and ending times of the report with the -e and -s
arguments with time specified in the format hh[:mm[:ss]]. The -i option selects records
at sec-second intervals. Otherwise, all intervals found in the data file are reported.

Note — The sum of CPU can vary slightly from 100 because
rounding errors in the production of a percentage figure.

![](bbox=[0.088, 0.246, 0.139, 0.273])

# Options

The following options modify the subsets of information reported by sar.

+   -a Report use of file-access routines iget/s, namei/s, dirblk/s.
-A Report all data. Equivalent to -abcdkgmpqruvy.
-b Report buffer activity:
  bread/s, bwrit/s
  Transfers per second of data between system buffers
  and disk or other block devices.
  lread/s, lwrit/s
  Accesses to system buffers.
  %rcache, %wcache
  Cache hit ratios, that is, (1-bread/read) as a
  percentage.
  pread/s, pwrit/s
  Transfers by raw (physical) device mechanism.
-c Report system calls.
  scall/s System calls of all types.
  sread/s, swrit/s, fork/s, exec/s
  Specific system calls.
  rchar/s, wchar/s
  Characters transferred by read and write system calls.
  Report no incoming or outgoing exec(2) or fork(2)
calls.
-d Report activity for each block device (for example, disk or tape device)
with the exception of XDC disks and tape drives. The device
sification dsk- is generally used to represent a disk drive. The device
sification used to represent a tape drive is machine dependent. The
activity data reported is: