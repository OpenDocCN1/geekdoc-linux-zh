# CHAPTER 7 Intel® VTune™ Amplifier XE

optional updates are designed for users interested in the latest functionality, recommended updates are designed for users interested in only updating occasionally.

At the time of this writing, a VTune license for noncommercial use on Linux can be obtained for free. For more information about both the tool and the commercial and noncommercial licensing, visit the VTune website at https://software.intel.com/en-us/vtune-amplifier-xe.

# 7.1 INSTALLATION AND CONFIGURATION

VTune provides its out-of-tree kernel drivers for collecting system information and programming the PMU. The source code for these drivers is shipped with VTune and can be found in the $VTUNE_INSTALL/sepdk/ directory. This allows for the driver modules to be built for the system's current kernel version.

As part of the default installation process, the installation script will automatically build the driver modules and install an init script that inserts the modules into the kernel at boot. One or both of these steps can be skipped during the installation by selecting to customize the installation and deselecting the desired steps. In order to be as portable as many distributions as possible, the script generated is designed to be compatible with the legacy it system. Modern systems, such as systemd, provide backward compatibility with these old style scripts, and therefore as well.

There are three modules that must be loaded before collection can begin. The first module, pax, handles multiplexing a single PMU between multiple processors. This driver creates a special device file in /dev/pax. Each VTune process that needs the PMU first open this device file and use ioctl(2) interface to reserve and unreserve the PMU for the given process. This locking mechanism prevents one from interfering with the profiling of another.

The second module, sep, handles the PMU event programming. It is often referenced as sepX_Y, where X and Y represent the major and minor driver numbers. The sep provides its own APIC interrupt handler for PMU events and handles all of the architectural-specific aspects of programming events and configuring the system for profiling. This driver creates a directory, /dev/sepX_Y/, where a special device file is created-cpu for sampling.

```
$ $1 /dev/sep3_1/
c0% m0% s1% s2% s3% s4% s5% s6% s7
```

The third module, vtsspp, is responsible for monitoring process execution. This driver records the specifics of the process being monitored, such as the stack traces, the registers, and so on. This information is correlated with the information from the PMU interrupts in order to attribute PMU events to ELF files, functions, and lines of code. This driver exposes a configuration directory within the proc filesystem for instance: