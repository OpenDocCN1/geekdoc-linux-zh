In practice, the opportunity to idle parts of the CPU only arises when the system isn’t busy. In those circumstances, the additional overhead of packing threads onto one core may have no detectable effect. Experiment to see if you can discern any difference with your specific workload.

The process scheduler’s power management system consults two control variables, both of which are set through files in the **/sys/devices/system/cpu** directory. The **sched_mc_power_savings** variable controls whether all cores on a CPU are used before activating another CPU, and the **sched_smt_power_savings** variable controls whether all thread slots on a core are used before activating another core. In both cases, a value of 0 turns power saving off and a 1 turns it on.

For example, to turn on both power-saving modes, you could use the commands

```
sudo sh -c 'echo 1 > /sys/devices/system/cpu/sched_mc_power_savings'
sudo sh -c 'echo 1 > /sys/devices/system/cpu/sched_smt_power_savings'
```

To make these changes persistent across reboots, check out the sysctl command or add the lines to a startup script such as **/etc/init.d/local** on Ubuntu or SUSE (create it if necessary) or **/etc/rc.local** on Red Hat.

A computer’s CPU is one of its most profligate consumers of energy (just look at those heat sinks!), so aggressive power management can significantly reduce the system’s power use.

# Filesystem power savings

You can save power and increase performance by preventing filesystems from maintaining a “last access” time (atime) for every file. This information isn’t very useful, and it theoretically adds a tax of one seek and one write to every file operation. (The real-world impact is harder to quantify because of block caching.)

Zedlewski et al. analyzed hard disk power consumption in a 2003 paper and concluded that seeks cost about 4 milliseconds each on an IBM Microdrive; the cost is probably at least double that for a standard drive with its larger armature. Combining the cost of seeks with the cost of writes, we calculate the benefit of disabling last access times to be up to several kWh per drive per year. Not a huge savings, but probably worthwhile for the performance benefits alone; the energy savings are just gravy.

On most filesystems, you can turn off maintenance of the last access time with the **noatime** option to **mount**:

```
sudo mount -o remount,noatime /
```

Some Linux systems also support the **relatime** mount option, which provides hybrid functionality. Under this option, last access time is only updated if the previous value is earlier than the file’s modification time. This mode allows tools such as mail readers to correctly identify cases in which an interesting file has been changed but not yet read.