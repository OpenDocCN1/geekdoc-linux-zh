As with any directory, start by looking at a detailed directory listing of /proc. To do so, log in as root and type ls -l /proc in a terminal window. In the output, the first set of directories (indicated by the letter d at the beginning of the line) represents the processes that are currently running on your system. Each directory that corresponds to a process has the process ID (a number) as its name.

![](bbox=[0.15, 0.32, 0.25, 0.45])

Notice also a very large file named /proc/kcore; that file represents the entire physical memory of your system. Although /proc/kcore appears in the listing as a huge file, no single physical file is occupying that much space on your hard drive — so don’t try to remove the file to reclaim disk space.

Several files and directories in /proc contain interesting information about your Red Hat Linux PC. The /proc/cpuinfo file, for example, lists the key characteristics of your system, such as processor type and floating-point processor information. You can view the processor information by typing cat /proc/cpuinfo. For example, here’s what I get when I type cat /proc/cpuinfo on my system:

```
processor		: 0
vendor_id		: GenuineIntel
cpu family		: 15
model			: 2
model name		: Mobile Intel(R) Celeron(R) CPU 1.50GHz
stepping		: 7
cpu MHz			: 1495.610
cache size		: 256 KB
fdiv_bug		: no
hlt_bug			: no
f00f_bug		: no
coma_bug		: no
fpu			: yes
fpu_exception	: yes
cpuid level		: 2
wp			: yes
flags			: fpu vme de pse tsc msr pae mce cx8 sep mtrr
			pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2
			ss ht tm
bogomips		: 2981.88
```

This output is from a 1.5 GHZ Celeron system. The listing shows many interesting characteristics of the processor. Notice the line that starts with fdiv_bug. Remember the infamous Pentium floating-point division bug? The bug is in an instruction called fdiv (for floating-point division). Thus, the fdiv_bug line indicates whether this particular Pentium has the bug (fortunately, my PC’s processor does not).