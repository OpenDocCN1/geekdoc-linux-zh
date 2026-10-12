In Example 3-2 we see that there is heavy paging taking place. In our case even the swap space is fully used up. It might be the cause of the degradation in the application transaction rate and response time, in which case Linux might be spending its CPU cycles on swapping in and out the pages. In this case we did a over commitment of memory to the affected Linux instance to improve the response time.

# Example 3-2 Gathering swap, memory, and CPU information using vmstat

```
lnx02:~ # vmstat 30
procs ---memory--- ---swap-- -----io----- -system-- ----cpu----
r b swpd free buff cache si so bi bo in cs us sy id wa st
0 0 713640 7784 1932 28644 0 0 0 7 152 142 0 0 99 0 0
0 0 713632 7784 1972 29096 1 0 1 5 158 141 0 0 99 0 0
0 0 713616 7536 2012 29040 1 0 1 8 159 143 0 0 99 0 0
0 0 713600 7536 2052 28984 1 0 1 3 161 140 0 0 99 0 0
0 0 713596 7412 2092 28916 1 0 1 8 156 143 0 0 99 0 0
0 0 713596 7412 2132 28876 0 0 0 2 152 140 0 0 99 0 0
0 0 719888 9144 2176 29316 1 210 1 217 257 142 0 98 2 0
0 0 718812 12976 2212 29316 122 26 122 32 186 174 1 0 97 1 0
0 0 718668 7340 2240 29228 360 164 360 172 270 259 1 1 93 5 0
1 0 719172 8764 2044 26808 789 453 789 456 360 339 2 2 86 10 0
0 0 718160 10364 808 21968 382 213 416 221 349 346 3 2 91 5 0
0 0 719400 10164 824 21124 264 200 264 202 425 366 3 1 92 4 0
```

# 3.1.3 System status (sysstat) tool

This package consists of several Linux tools to collect system data. The sysstat package is a widely used Linux standard tool. It is included in your distribution or can be downloaded from the Web:

http://pagesperso-orange.fr/sebastien.godard/

If you install the source package, you must compile the package on Linux on System z to use it. The sysstat package consists of the following components:

+   - sar reporting tool - reads binary file created with 'sadc' and converts it to readable output
+   - sadc data gatherer - stores data in binary file
+   - iostat - I/O utilization
+   - mpstat - processor utilization