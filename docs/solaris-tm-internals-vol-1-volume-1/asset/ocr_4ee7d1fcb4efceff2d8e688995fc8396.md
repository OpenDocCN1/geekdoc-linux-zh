![](bbox=[0.107, 0.131, 0.915, 0.707])

free = free memory measured in pages

# Global Paging Counters

re = pages reclaimed from the free list  
mf = minor faults – the page was in memory but was not mapped  
pi = pages paged in from file system or swap device  
po = pages paged out to file system or swap device  
fr = pages that have been destroyed or freed  
de = pages freed after writes

# Executable Paging Counters

epi = executable and library pages that are paged in  
epo = executable and library pages that are paged out (should be zero)  
epf = executable and library pages that are freed

# Anonymous Paging Counters

api = anonymous pages that are paged in from swap  
apo = anonymous pages that are paged out to swap  
apf = anonymous pages that are freed

# File Paging Counters

fpi = file pages that are paged in  
fpo = file pages that are paged out  
fpf = file pages that are freed

# CPU Summary

us = user cpu time  
sy = kernel cpu time  
wt = wait cpu time  
id = idle cpu time

```
```text
# memstat 3

memory -------- paging -------- executable - - anonymous --- fileys --- cpu
       free  re  mf   pi   po   fr  de  sr  epi  epo  epf  api  apo  apf  fpi  fpo  fpf  sys  wt  id
16128    8   0  341 1629 1677   0  18   0    0    0    0    0    0  341 1629 1677   4  35  34  27
15184   12   0  354 1720 2434   0 437   0    0    2    0   85   88  354 1634 2434   1  19  35  45
15152    6   0  160 1522 2541   0 490   0    0   16   85  114  160 1347 2414 2480   1  20  40  38
14968   19   0  162 1688 3285   0 698   0    0   18    0  168  181 162 1520 3085   1  29  34  36
15184   23 192  242 2232 3573   0 595   0    0   16    0  128  149  242 2104 3080   2  27  33  38
15704    8   0  194  480  581   0  53   0    0    0    0    0    0  194  480  581   1  16  46  38
16192   16  15  202  189  189   0   0   0    0    0    0    0    0  202  189  189   1  11  41  47
16976    4  54  200   40   40   0   0   0    0    0    0    0    0  200   40   40   1  16  37  46
17376    1  83  194    2    2   0   0   0    0    0    0    0    0  194    2    2   2  14  39  44
```
```

The columns for the memstat command are described in Table 7-8.

# Table 7-8  *Statistics from the memstat Command*

| Counter | Description |
|---|---|
| free | The amount of free memory as reported by `vmstat`, which reports the combined size of the cache list and free list. Free memory on Solaris 7 may contain some of the file system cache. |