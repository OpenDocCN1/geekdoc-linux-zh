If you now monitor the running frequency by looking at */sys/devices/system/cpu/cpu0/cpufreq/cpuinfo_cur_freq*, you will see it dancing to the tune of the CPU load.

The CPU scaling code lives in the *drivers/cpufreq/* directory. Look at *Documentation/cpu-freq/* for the detailed semantics of cpufreq sysfs nodes.