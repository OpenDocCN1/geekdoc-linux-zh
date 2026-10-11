The runlevel-based SysVinit daemon (**sysvinit** package) uses runlevels (single-user, multiuser, and more) and links from the `/etc/rc/2.d` directories to the init scripts in `/etc/init.d` to start and stop system services. The event-based Upstart init daemon uses events to start and stop system services. With version 9, Fedora switched to the Upstart init daemon and began the transition from the SysVinit setup to the Upstart setup. This section discusses Upstart and the parts of SysVinit that remain: the `/etc/rc2.d` and `/etc/init.d` directories and the concept of runlevels.

The Upstart init daemon is event based and runs specified programs when something on the system changes. These programs, which are frequently scripts, start and stop services. This setup is similar in concept to the links to init scripts that SysVinit calls as a system enters runlevels, except Upstart is more flexible. Instead of starting and stopping services only when the runlevel changes, Upstart can start and stop services upon receiving information that something on the system has changed. Such a change is called an *event*. For example, Upstart can take action when it learns from `udev` (page 482) that a filesystem, printer, or other device has been added or removed from the running system. It can also start and stop services when the system boots, when the system is shut down, or when a job changes state.

Future of Upstart
Changing from SysVinit to Upstart involves many parts of the Linux system. To make the switch smoothly and to introduce as few errors as possible, the Upstart team elected to make this transition over several releases.
Over time, Fedora will move away from the SysVinit setup and toward the cleaner, more flexible Upstart setup. As more system services are put under the control of Upstart, entries in the `/etc/event.d` directory will replace the contents of the `/etc/init.d` and `/etc/rc*.d` directories. Runlevels will no longer be a formal feature of Fedora, although they will be maintained for compatibility with third-party software. Eventually Upstart will also replace `crond`.

Software package
The Upstart system uses the `upstart` package, which is installed by default. Some of the files Upstart uses are found in the `initscripts` package, which is also installed by default.

# DEFINITIONS

**Events**
An *event* is a change in state that **init** can be informed of. Almost any change in state—either internal or external to the system—can trigger an event. For example, the boot loader triggers the **startup** event, the system entering runlevel 2 triggers the **runlevel 2** event, and a filesystem being mounted triggers the **path-mounted** event. Removing and installing a hotplug or USB device (such as a printer) can trigger an event. You can also trigger an event manually by giving the `initctl emit` command (page 421).

**Jobs**
A *job* is a series of instructions that **init** reads. These instructions typically include a program (binary file or shell script) and the name of an event. The **Upstart** init daemon runs the program when the event is triggered. You can run and stop a job manually giving the `initctl start` and `stop` commands, respectively (page 421). Jobs are divided into tasks and services.