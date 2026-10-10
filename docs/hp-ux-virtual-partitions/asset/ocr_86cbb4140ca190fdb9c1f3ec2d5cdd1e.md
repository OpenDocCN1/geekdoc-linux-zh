Plus was started or since the process was started. Disk I/O can mean a lot of different things. Disk I/O could mean taking blocks of data off the disk for the first time and putting them in RAM, or it could be entirely paging and swapping. Some processes will simply require a lot more Disk I/O than others. When this number is very high, however, take a close look at whether or not you have enough RAM. Keep in mind that pageout activity, such as deactivation and swapping, are attributed to the *vhand* process.

# RSS Size

The amount of RAM in KBytes that is consumed by the process. This is called the Resident Size. Everything related to the process that is in RAM is included in this column, such as the process's data, stack, text, and shared memory segments. This is a good column to inspect. Because slow systems are often erroneously assumed to be CPU-bound, I always make a point of looking at this column to identify the amount of RAM that the primary applications are using. This is often revealing. Some applications use a small amount of RAM but use large data sets, a point often overlooked when RAM calculations are made. This column shows all the RAM your process is currently using.

# Block On

The reason the process was blocked (unable to run). If the process is currently blocked, you will see why. If the process is running, you will see why it was last blocked. There are many reasons a process could be blocked. After *Thd Cnt* is a list of the most common reasons for the process being blocked.

# Thd Cnt

The total number of threads for this current process.