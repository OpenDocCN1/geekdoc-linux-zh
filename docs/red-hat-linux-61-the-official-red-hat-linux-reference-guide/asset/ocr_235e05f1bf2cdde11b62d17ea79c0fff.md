# Chapter 5. The proc System

If RAID support is compiled into the kernel, a /proc/sys/dev/raid/ directory will be available with at least two files in: speed_limit_min and speed_limit_max. These settings determine the acceleration of RAID devices for I/O intensive tasks, such as resyncing the disks.

# 5.3.9.2. /proc/sys/fs/

This directory contains an array of options and information concerning various aspects of the file system, including quota, file handle, inode, and entry information.nThe binfmt_misc directory is used to provide kernel support for miscellaneous binary formats.nThe important files in /proc/sys/fs/ include:

+   - density-state — Provides the status of the directory cache. The file looks similar to:
57411 52939 45 0 0 0
nThe first number reveals the total number of directory cache entries, the second number displays the number of unused entries. The third number shows the number of seconds between a directory has been freed and when it can be reclaimed, and the fourth the pages requested by the system. The last two are not used and display only zeros.
- dquot-nr — Shows the number of cached dquot entries.
- file-max — Change the maximum number of file handles that the kernel will allocate. Raising the value in this file can resolve errors caused by a lack of available file handles.
- file-nr — Displays the number of allocated file handles, used file handles, and the maximum number of file handles.
- overflowuid — Defines the fixed group ID and user ID, respectively, for use with file systems that only support 16-bit group user IDs.
- super-max — Controls the maximum number of superblocks available.
- super-nr — Displays the current number of superblocks in use.

# 5.3.9.3. /proc/sys/kernel/

This directory contains a variety of configuration files that directly affect the operation of the kernel. Some of the most important files include:

+   - acct — Controls the suspension of process accounting based on the percentage of free space available on the file system containing the log. By default, the file looks like this:
2 30
The second value sets the threshold percentage of free space when logging will be suspended, while the first value dictates the percentage of free space for logging to resume. The third value sets the interval, at the kernel polls the file system to see if logging should be suspended or resumed.
- cap-bound — Controls the capability bounding settings, which provides a list of capabilities for any process on the system. If a capability is not listed here, then no process, may gain it. The idea is to make the system more secure by ensuring that certain things cannot happen, at beyond a certain point in the boot process.

For a valid list of values for this virtual file, consult /usr/src/linux-2.4/include/linux/capability.h. More information on capability bounding is available at the following URL: http://lwn.net/1999/1202/kernel.php3.