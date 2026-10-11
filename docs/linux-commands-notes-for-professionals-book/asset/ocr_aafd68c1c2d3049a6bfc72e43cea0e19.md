```
model          : 15
model name     : Intel(R) Core(TM)2 Quad CPU  Q6600 @ 2.40GHz
stepping       : 11
cpu MHz        : 1596.000
cache size     : 4096 KB
physical id    : 0
siblings       : 4
core id        : 3
cpu cores      : 4
apicid         : 3
initial apicid : 3
fpu            : yes
fpu exception  : yes
cpuid level    : 10
wp             : yes
flags          : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts
acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx lm constant_tsc arch_perfmon pni pebs bts rep_good pni
dtes64 monitor ds_cpl vmx est tm2 ssse3 cx16 xtpr pdcm lahf_lm tpr_shadow vnmi flexpriority
bogomips       : 4800.30
cflush size    : 64
cache_alignment : 64
address sizes  : 36 bits physical, 48 bits virtual
power management:
```

**count processor (including cores):**

```
`$ grep -c processor /proc/cpuinfo`
```

# # Section 6.5: Process monitoring and information gathering

Overall you have two ways to monitor processes at linux host

**Static monitoring**

Most widely used command is *ps* (i.e., process status) command is used to provide information about the currently running processes, including their process identification numbers (PIDs).

Here few useful options to gather specific information.

List processes in a hierarchy

```
`$ ps -e -o pid,args --forest`
```

List processes sorted by % cpu usage

```
`$ ps -e -o pcpu,cpu,nice,state,cputime,args --sort pcpu | sed '/^ 0.0 /d'`
```

List processes sorted by mem (KB) usage.

```
`$ ps -e -orss=,args= | sort -b -k1,1n | pr -T$COLUMNS`
```

List all threads for a particular process (“firefox-bin” process in example )

```
`$ ps -C firefox-bin -L -o pid,tid,pcpu,state`
```

After finding specific process you can gather information related to it using *lsof* to list paths that process id has open