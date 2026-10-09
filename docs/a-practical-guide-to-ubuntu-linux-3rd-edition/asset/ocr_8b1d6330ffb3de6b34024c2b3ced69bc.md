/etc/init.d to start and stop system services (page 440). The event-based Upstart init daemon uses events to start and stop system services. With the Feisty release (7.04), Ubuntu switched to the Upstart init daemon and began making the transition from the SysVinit setup to the Upstart setup. This section discusses Upstart and the parts of SysVinit that remain: the /etc/rc?.d and /etc/init.d directories and the concept of runlevels. See the tip about terminology on page 445.

The Upstart init daemon is event based and runs specified programs when something on the system changes. These programs, which are frequently scripts, start and stop services. This setup is similar in concept to the links to init scripts that SysVinit calls as a system enters runlevels, except Upstart is more flexible. Instead of starting and stopping services only when the runlevel changes, Upstart can start and stop services upon receiving information that something on the system has changed. Such a change is called an event. For example, Upstart can take action when it learns from udev (page 502) that a filesystem, printer, or other device has been added or removed from the running system. It can also start and stop services when the system boots, when the system is shut down, or when a job changes state.

Changing from SysVinit to Upstart involves many parts of the Linux system. To make the switch smoothly and to introduce as few errors as possible, the Upstart team elected to make this transition over several releases.

Ubuntu has been moving away from the SysVinit setup and toward the cleaner, more flexible Upstart setup. As more system services are put under the control of Upstart, entries in the /etc/init directory (see the tip on page 440) will replace the contents of the /etc/init.d and /etc/rc?.d directories. Runlevels will no longer be a formal feature of Ubuntu, although they will be maintained for compatibility with third-party software. Eventually Upstart will also replace crond.

# SOFTWARE PACKAGE

The Upstart system is contained in one package, which is installed by default:

+   * upstart—Provides the Upstart init daemon and initctl utility.

# DEFINITIONS

An event is a change in state that can be communicated to init. Almost any change in state—either internal or external to the system—can trigger an event. For example, the boot loader triggers the startup event (startup man page) and the telinit command (page 444) triggers the runlevel event (page 444). Removing and installing a hotplug (page 502) or USB device (such as a printer) can trigger an event as well. You can also trigger an event manually by giving the initctl emit command (page 436). For more information refer to “Events” on page 437.

A job is a series of instructions that init reads. These instructions typically include a program (binary file or shell script) and the name of an event. The Upstart init daemon runs the program when the event is triggered. You can run and stop a job manually by giving the initctl start and stop commands, respectively (page 436).