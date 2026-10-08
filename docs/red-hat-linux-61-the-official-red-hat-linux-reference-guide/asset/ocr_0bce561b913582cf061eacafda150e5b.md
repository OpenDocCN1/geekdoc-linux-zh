# Chapter 5. The proc File System

# 5.2.1. /proc/apm

This file provides information about the state of the Advanced Power Management (APM) system and is used by the apm command. If a system with no battery is connected to an AC power source, this virtual file will look like this:

```
1.16 1.2 0x07 0x01 0xff 0x80 -1 ?
```

Running the apm -v command on such a result produces output similar to this:

```
APM BIOS 1.2 (kernel driver 1.16)
AC on-line, no system battery
```

For systems which do not use a battery as a power source, apm is able to do little more than put the machine in standby mode. The apm command is much more useful on laptops. For example, the following output is from cat /proc/apm on a laptop running Red Hat Linux plugged into a power outlet:

```
1.16 1.2 0x03 0x01 0x03 0x09 100% -1 ?
```

When the system is unplugged from its power source for a few minutes, the contents of the apm file change to something like this:

```
1.16 1.2 0x02 0x00 0x00 0x01 99% 1792 min
```

The apm -v command will now yield more useful data, such as the following:

```
APM BIOS 1.2 (kernel driver 1.16)
AC off-line, battery status high: 99% (1 day, 5:52)
```

# 5.2.2. /proc/cmdline

This file shows the parameters passed to the kernel at the time it is started. A sample /proc/cmdline file looks like this:

```
root=/dev/hda2
```

This tells us that the kernel is mounted read-only (signed by (ro)) off the second partition on the first IDE device (/dev/hda2).

# 5.2.3. /proc/cpuinfo

This virtual file identifies the type of processor used by your system. The following is an example of the output typical /proc/cpuinfo:

```
processor : 0
vendor_id : AuthenticAMD
cpu family : 5
model : 9
name : AMD-K6 (tm) 3D+ Processor
stepping : 1
cpu MHz : 400.918
cache size : 256 KB
div_bug : no
hlt_bug : no
```