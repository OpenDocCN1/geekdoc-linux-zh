# 160 CHAPTER 8 Perf

# 8.2.2 PERF STAT

perf stat tool counts the specified performance counters for the given process or processes. This provides the ability to calculate the necessary metrics in order to determine where further analysis should focus, and also for the comparison of multiple implementations.

As mentioned in Section 5.2.2, each counter value represents one member of a sample that estimates the infinite population. As the number of samples increases, the more accurate the sample becomes. To accommodate this, perf stat supports a -repeat command line argument, which causes the measurement to be performed N times, with the average and standard deviation reported.

If no events are specified, the default events, including the "task-clock," "wall-clock," and the number of "context-switches," "migrations," "page-faults," "cycles," "stalled-cycles-frontend," "stalled-cycles-backend," "instructions," "branches," and "branch-misses," are chosen.

For instance, to calculate the CPI, instructions for compressing a Linux tarball with gzip, at the default compression ratio:

```
$ perf stat -repeat 20 -e "cycles,instructions:u" gzip -c \
 /dev/shm/linux-3.15.tar /dev/null
```

Performance counter stats for "gzip -c /dev/shm/linux-3.15.tar" (20 runs):

```
58,559,095,434 cycles:u @ 0.000 GHz (+ 0.09%)
86,967,639,500 instructions:u @ 1.49 insns per cycle (+ 0.00%)
```

17,984.389393 time elapsed (+ 0.08%)

CPI, 86,967,639,500 = 0.67. Notice that the standard deviation is reported at the end of the line for each event. As mentioned in Chapter 6, it's important to only correlate events collected together. Notice that the events calculated together are included within the same event group. It would be incorrect to calculate the CPI with the cycles from one run of perf stat, and the instructions from a different run.

# 8.2.3 PERF RECORD, PER REPORT, AND PER TOP

Once the counting of values identifies the bottleneck, sampling can be used to determine what instructions are responsible. Use perf record or perf top. The main difference between the two is that perf top dynamically displays the results of the samples collected, updating as new samples are collected. The delay between updates is controlled with the -d command line argument, taking as an the number of seconds between refreshes.

On the other hand, perf record saves the sampling data into a file, which can then be manipulated once all of the data collection has completed. By default, the data file will be created using perf.data. If that file already exists, the existing file will be