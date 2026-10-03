# Linux Hack

Ajay Kumar Tiwari

# Chapter 12: System Monitoring and Performance

# Hack 89. Free command

free command displays all the necessary information about system physical (RAM) and swap memory.

Syntax: free [options]

What is the total RAM on my system?

In the example below, the total physical memory on this system is 1GB. The values displayed below are in KB.

```
# free
  totalused
Mem: 10346241006696
-/+ buffers/cache:
Swap:2031608
freeshared buffers
27928 0174136
216668817956
02031608
cached
615892
```

What is the total memory on my system including RAM and Swap?

In the following command:

o
o

option m displays the values in MB

option t displays the “Total” line, which is sum of physical and swap memory values