# CHAPTER 3 Intel® Core™ Processors

User space applications do not need to worry about explicitly controlling the P state unless specifically wanted to. Within the Linux kernel, the CPU frequency scaling driver, CONFIG_CPU_FREQ, has traditionally been responsible for controlling the system's P state transitions. This driver supports multiple governors for controlling the desired management policy. At the time of this writing, there are five governors:

+   1. Performance (CONFIG_CPU_FREQ_GOV_PERFORMANCE)
2. Powersave (CONFIG_CPU_FREQ_GOV_POWERSAVE)
3. Userspace (CONFIG_CPU_FREQ_GOV_USERSPACE)
4. Ondemand (CONFIG_CPU_FREQ_GOV_ONDEMAND)
5. Conservative (CONFIG_CPU_FREQ_GOV_CONSERVATIVE)

The performance governor maintains the highest processor available. The powersave governor defers the policy to user space, allowing for an application or daemon to manually set the frequency. The ondemand governor monitors the processor utilization and adjusts the frequency accordingly. Finally, the conservative governor is similar to the ondemand governor but additionally attempts to avoid frequent state changes. Due to the concept of race-to-idle, as introduced in the Introduction chapter, the ondemand governor has typically provided the best power savings on Intel Architectures.

One of the challenges with this driver has been tuning the algorithm for specific hardware generations. In order to remedy this, a new and more efficient P state driver, the Intel® P state driver, was written by Dirk Brandewe. Unlike the previous driver, this one checks the processor generation and tunes accordingly.

The current frequency driver can be determined by checking the /sys/devices/system/cpu/ directory. If the cpufreq driver is active, a cpufreq directory will be present, whereas if the Intel P state driver is active, an intel_pstate directory will be present. Within these sysfs directories are the tunables exposed to user space by these drivers.

# C states

While the core's frequency reduces power consumption, dropping the frequency to zero provides greater savings. C states are the results of the observation that the processor cores in client systems idle most of the time. Therefore, running the core at its lowest possible frequency is better than running it at its highest, it's even better to simply turn it off.

The ACPI specification also defines the concept of processor power states. As of the latest ACPI specification, the states are defined as:

+   C0 "While the processor is in this state, it executes instructions" (Unified EFI, Inc., 2014).
C1 "This processor power state has the lowest latency. The hardware latency in this state must be low enough that the operating software does not consider