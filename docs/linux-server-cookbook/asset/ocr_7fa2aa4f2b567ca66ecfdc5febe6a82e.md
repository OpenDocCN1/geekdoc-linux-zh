![](bbox=[0.15, 0.08, 0.86, 0.28])

Figure 6.32: Output example for the command lsblk

# Command iostat

This command part of the sysstat package, described previously for the CPU usage, is usually used for the input/output statistics. The statistics show the physical storage devices, the number of transfers (tps) per second, the data read and write data per second, and the data read and written in the period observed. Figure 6.33 shows the output example; option -y excludes the first entry related to the average from the system that was booted:

![](bbox=[0.15, 0.5, 0.86, 0.7])

Figure 6.33: Output example for the command iostat

# Command iotop

This utility is similar to the top command but related to the Input/Output only. This tool should be installed (iotop package). Figure 6.34 shows the aspect of the application: