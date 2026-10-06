# Adding PMU support to Raspbian for the Generation 1 Raspberry Pi

The Linux kernel included in the Raspbian Linux distribution through its December 2014 release does not support for the ARM11 Performance Monitoring Unit through Linux's perf_event API. Fortunately, it is relatively easy to patch the kernel to enable this feature. This patch was developed by Chad Paradis and Vincent M. Weaver of the University of Maine.

To check if your kernel supports perf_event, check to see if the directory /sys/bus/event_source/ contains any files except “breakpoint” and “software”. On the Raspberry Pi, the existence of the symbolic link named “v6” indicates support for perf_event.

To enable support you must make a minor change to two kernel source files and recompile the kernel. Compiling the Linux kernel requires an unreasonable amount of time if performed on the Raspberry Pi itself, so it is best to do this by cross-compiling on a capable Linux workstation.

# A.1 DOWNLOAD THE LINUX KERNEL AND CROSS-COMP TOOLS

The Raspbian kernel is available for download on GitHub https://github.com/raspberrypypil/linux.git. You should download the same kernel version as currently running on your Raspberry Pi. You can check your kernel version using the uname -a command on the Raspberry Pi.

This kernel repository is usually several versions ahead of the kernel installed in the latest version of Raspbian, but you can use the “git clone