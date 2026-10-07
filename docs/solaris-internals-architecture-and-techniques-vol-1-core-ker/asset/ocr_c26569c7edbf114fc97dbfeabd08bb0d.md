free = free memory measured in pages

# Global Page Counters

re = pages reclaimed from the free list
mf = minor faults - the page was in memory but not mapped\pi = pages paged in from file system or swap device\spo = pages paged out to file system or swap device
de = pages that have been destroyed or freed

# Executable Page Counters

epi = executable and library pages that are paged in
epo = executable and library pages that are paged out (should be zero)
epf = executable and library pages that are freed

# CPU Summary

us = user cpu time
sky = kernel cpu time
wt = wait cpu time
d = idle cpu time

# Anonymous Page Counters

api = anonymous pages that are paged in swap
apo = anonymous pages that are paged out to swap
pf = anonymous pages that are freed

# File Page Counters

api = file pages that are paged in
apo = file pages that are paged out
pf = file pages that are freed

![](bbox=[0.107, 0.497, 0.933, 0.687])

| memory free re mf pi po fr de re epi epo epf apo fpi fpo wpo us ky wt id |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---||
| 16128 | 8 | 0 | 341 | 1629 | 1677 | 0 | 0 | 0 | 0 | 0 | 0 | 85 | 88 | 341 | 1629 | 1677 | 45 | 34 | 27 |
| 15184 | 12 | 0 | 350 | 1720 | 2434 | 0 | 437 | 0 | 0 | 2 | 0 | 85 | 81 11 | 1634 | 2334 | 19 | 35 | 43 |
| 15152 | 6 | 0 | 160 | 1520 | 2541 | 0 | 490 | 0 | 0 | 16 | 85 | 114 | 1605 | 1430 | 241 | 22 | 40 | 38 |
| 14968 | 19 | 0 | 162 | 1688 | 3285 | 0 | 698 | 0 | 06 | 68 | 181 | 1622 | 1520 | 385 | 21 | 29 | 34 | 36 |
| 15386 | 23 | 19 | 242 | 2232 | 3573 | 0 | 595 | 0 | 06 | 12 | 149 | 204 | 2119 | 273 | 27 | 32 | 35 | |
| 15704 | 8 | 0 | 194 | 2102 | 3960 | 0 | 0 | 0 | 0 | 0 | 200 | 394 | 581 | 11 | 41 | 46 | 38 |
| 16192 | 16 | 5 | 202 | 1889 | 190 | 0 | 0 | 0 | 0 | 0 | 200 | 202 | 189 | 11 | 41 | 47 | 44 |
| 16976 | 4 | 54 | 200 | 40 | 40 | 0 | 0 | 0 | 0 | 0 | 200 | 40 | 1 | 16 | 37 | 46 | | |
| 17376 | 1 | 8 | 194 | 2 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 194 | 40 | 2 | 14 | 39 | 44 |

The columns for the memstat command are described in Table 7-8.

| Counter | Description |
|---|---|
| free | The amount of free memory as reported by vmstat, which reports the bins size of the cache and free list. memory on Solaris 7 may contain some of the file system cache |