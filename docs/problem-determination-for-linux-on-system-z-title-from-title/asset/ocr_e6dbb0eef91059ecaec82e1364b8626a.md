# 3.1.10 OProfile

OProfile is an open source profiler for Linux systems. It offers profiling of all running code on a Linux system, including the kernel, shared libraries, application binaries, and so on, and provides a variety of statistics at a low overhead (varying from 1–8%) depending on the workload. It is released under the GNU GPL. OProfile consists of a kernel driver, a daemon for collecting sample data, and tools for report generation.

OProfile is generally supported in Linux kernel 2.2, 2.4, 2.6, and later. But, for Linux on System z, OProfile only supports kernel 2.6 or later. For SUSE Linux, the kernel level must be at least kernel-s390(x)-2.6.5-7.191, which starts from SLES9 SP2. For Red Hat Linux, the kernel level must be at least kernel-2.6.9-22.EL, which is RHEL4 U2.

OProfile utilizes CPU's performance counters to count events for all of the running code, and aggregates the information into profiles for each binary image. However, System z hardware currently does not have support for this kind of hardware performance counters utilized by OProfile, so the timer interrupt is used instead.

Using OProfile the code can be profiled for:

+   - Hardware and software interrupt handlers
+   - Kernel modules, the kernel
+   - Shared libraries
+   - Applications

OProfile setup involves configuring the kernel source by enabling the profiling option. To build and install OProfile, issue the commands shown in Example 3-16 from the decompressed oprofile directory. As shown in this example, we used the option *with-kernel-support*. You would use this option when you have a kernel Version of 2.6 and later. For more information about installation instructions of OProfile, see:

http://oprofile.sourceforge.net/doc/install.html

# Example 3-16 Setting up OProfile

```
./configure --with-kernel-support
make
make install
```