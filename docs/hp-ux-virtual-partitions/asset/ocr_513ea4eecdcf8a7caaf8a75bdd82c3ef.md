I use **set -x** in this file to turn on execution tracing. I always do this when first debugging a shell program so I can see that the lines in the shell program as they are executed. The line being executed will appear with a "+" in front of it, followed by what you would normally see when the program is run. **The read a** is a way of pausing the program to wait for input so I can review what has been run to that point of the program.

In order for this program to run, we must slightly modify the file containing the primary disk devices and add the volume group number to the beginning of each line. In addition, I decided to call the program from the file that has the primary disks in it and operate on one line of disks at a time. The following listing shows the updated file containing the name of the shell program in the previous listing (**vg.sh**), followed by the volume group number and then the list of five primary disks names for each volume group:

```
```
#vg.sh 01 c9t0d0 c9t0d1 c9t0d2 c8t0d0 c8t0d1
#read a
#vg.sh 02 c7t0d0 c7t0d1 c7t0d2 c10t0d0 c10t0d1
#read a
#vg.sh 03 c9t0d3 c9t0d4 c9t0d5 c8t0d3 c8t0d4
#read a
#vg.sh 04 c7t0d3 c7t0d4 c7t0d5 c10t0d3 c10t0d4
#read a
#vg.sh 05 c9t0d6 c9t0d7 c9t1d0 c8t0d6 c8t0d7
#read a
#vg.sh 06 c7t0d6 c7t0d7 c7t1d0 c10t0d6 c10t0d7
#read a
#vg.sh 07 c9t1d1 c9t1d2 c9t1d3 c8t1d1 c8t1d2
#read a
#vg.sh 08 c7t1d1 c7t1d2 c7t1d3 c10t1d1 c10t1d2
#read a
#vg.sh 09 c9t1d4 c9t1d5 c9t1d6 c8t1d4 c8t1d5
#read a
#vg.sh 10 c7t1d4 c7t1d5 c7t1d6 c10t1d4 c10t1d5
```
```

**The read a** between lines of this file will pause and wait for you to enter a **Return** before the next line will be executed. I did this in case I decided to run several lines and I wanted to check the results between the execution of lines.

We can now uncomment the first line of the file and type the file name **pri**, which will call **vg.sh** and run the program (you must give appropriate permissions to the files and make sure both **vg.sh** and **pri** are executable.) I