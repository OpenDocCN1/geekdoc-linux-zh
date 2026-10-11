To view the information that Linux has detected regarding the CPU in the computer, simply view the contents of the cpuinfo file in the /proc directory:

```
[root@server1 root]# cat /proc/cpuinfo
processor : 0
vendor_id : GenuineIntel
cpu family : 6
model : 8
model name : Pentium III (Coppermine)
stepping : 10
cpu MHz : 800.049
cache size : 256 KB
fdiv_bug : no
hlt_bug : no
f00f_bug : no
coma_bug : no
fpu : yes
fpu_exception : yes
cpuid level : 2
wp : yes
flags : fpu vme de pse tsc msr pae mce cx8 mmtr pge mca cmov pat pse36 mmx fxsr
sse
bogomips : 1585.15
[root@server1 root]#
```

The preceding output indicates that there is only one processor that runs at 800MHz (approximately) and has 256KB of processor cache. If, for example, the computer in actually has two processors instead of one, Linux has failed to detect the second processor. In this case, you might need to change a setting in BIOS or research a solution to the problem on the motherboard or processor manufacturer's Web site.

It is also important to ensure that Linux has detected the correct amount of RAM in the system after installation. To do this, you can view the contents of the /proc/meminfo file, as shown in the following output:

```
[root@server1 root]# cat /proc/meminfo
MemTotal: 257108 kB
MemFree: 10116 kB
Buffers: 24668 kB
Cached: 54032 kB
SwapCached: 2876 kB
Active: 164472 kB
Inactive: 27132 kB
HighTotal: 0 kB
HighFree: 0 kB
```