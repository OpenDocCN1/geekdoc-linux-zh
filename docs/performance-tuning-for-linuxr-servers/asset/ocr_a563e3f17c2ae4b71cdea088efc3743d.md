# ## System Initialization: BSD Versus System V Initialization

System initialization starts where the kernel bootup ends. The first program that the kernel runs is the init process. The init process reads the system initialization table (/etc/inittab) to see how various daemons need to be initialized and started. This section examines how system initialization works in Linux.

The various Linux distributions have adopted two system initialization styles. Red Hat and Debian use the System V initialization type. Others, such as Slackware, use the BSD style.

The Filesystem Hierarchy Standard (FHS) v2.0 for Linux states that either BSD- or System V-style initialization is acceptable. The standard stopped short, however, of outlining exactly where the rc scripts would go, except to say that they would be below /etc. Future revisions to the standard might provide further guidance.

Under system initialization, the biggest difference between BSD and System V is the init scripts. With BSD style, all daemons are started essentially by only a few scripts. For example, the init process in Slackware, which adopts the BSD style, runs the system script (/etc/rc.d/rc.S) to prepare the system. The rc.S file enables the system's virtual memory, mounts necessary file systems, cleans up certain log directories, initializes Plug and Play devices, loads kernel modules, configures PCMCIA devices, and sets up serial ports. The local script (rc.local) is available for system administrators to tailor to the specific system on which it is running. The system and local scripts can, in turn, call other scripts to accomplish their objectives, but they are called by the init process sequentially.

Many other Linux distributions make use of System V style instead of the BSD style. Unlike the BSD style, the System V scripts are independent, stand-alone initialization scripts. They make use of runlevels that correspond to different groups of processes or tasks to be executed. The scripts are run from runlevels 0 to 6 by default, even though several runlevels are not used. In other words, each runlevel is given a subdirectory for init scripts that allows for maximum flexibility in initializing the system and necessary daemons. The BSD style, by having only a few scripts to start everything, does not allow for the kind of flexibility System V brings. It does, however, make things easier to find.

It should be noted that, even though Slackware adopts the BSD-style system initialization, it does provide System V initialization compatibility. In fact, many Linux distributions use the same init binary, so the difference is not that great between various Linux distributions when it comes to system initialization.

# ## Initialization Table (/etc/inittab)

As mentioned earlier, the system initialization table (/etc/inittab) specifies to the init process how to initialize and start various daemons during system bootup. Comments in /etc/inittab are preceded by # and are skipped over by the init process. Non-comment lines in /etc/inittab have the following format: