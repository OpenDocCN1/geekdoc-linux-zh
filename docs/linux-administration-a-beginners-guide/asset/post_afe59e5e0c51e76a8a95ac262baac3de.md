
## Issues on High-Volume Servers

Like any operating system, Linux has finite resources. If the system begins to run short of resources while servicing requests (such as Web access requests), it will begin refusing new service requests.

The following entries in /proc allow you to handle a larger load:

- /proc/sys/fs/file-max
- /proc/sys/net/ipv4/ip_local_port_range
- /proc/sys/net/ipv4/tcp_max_syn_backlog

The first entry in this list, /proc/sys/fs/file-max, specifies the maximum number of open files that Linux can support at any one time. The default value is 4096, but this may be quickly exhausted on a very busy system with a lot of network connections. Raising it to a larger number, such as 8192 or 16384, will help.

If you are increasing the number of possible open files, you will need to increase the available ports your system can use. The lower and upper boundaries are set in the /proc/sys/net/ipv4/ip_local_port_range file; defaults are 1024 (lower) and 4096 (upper), respectively. On a loaded system, you'll want to change these defaults to 31000 and 61000 by adding the following line to the end of your /etc/rc.d/rc.local boot file:

```bash
echo "31000 61000" > /proc/sys/net/ipv4/ip_local_port_range
```

Finally, if you're getting a large number of connections, you're getting them quickly as well. A burst of new connections can easily take some time to handle, and those connections on the queue must wait. As the queue grows, so does the possibility that your queue will run out of space. The default length of the queue is 128 connections. You can increase it if you see connections getting refused on a regular basis.

> NOTE: Before changing the length of the connection queue, be sure to look at your server process first. Make sure the reason your system is refusing connections isn't because the CPU load is too high. If that's the case, increasing the number of available connections isn't going to help. You can monitor CPU utilization with the vmstat command; read the man page on it for more information.

## Debugging Hardware Conflicts

Debugging hardware conflicts is always a chore. You can ease the burden by using some of the entries in /proc. These two entries are specifically designed to tell you what's going on with your hardware:

- /proc/pci, which details all the PCI devices in your system—very handy when you don’t know the make and model of a device and you don’t want to have to open the machine!
- /proc/ioports, which tells you the relationships of devices to I/O ports, and whether there are any conflicts. With PCI devices becoming dominant, this isn’t a big issue. Nevertheless, as long as you can buy a new motherboard with ISA slots, you’ll always want to have this option.

## SUMMARY

In this chapter, we learned about the /proc file system and how we can use it to get a peek inside the Linux kernel as well as to influence the kernel’s operation. The tools used to accomplish these tasks are relatively trivial (echo and cat), but the concept of a pseudo-file system that doesn’t exist on disk can be a little difficult to grasp.

Looking at /proc from a system administrator’s point of view, we learned to find our way around the /proc file system, and how to get reports from various subsystems (especially the networking subsystem). We learned how to set kernel parameters to accommodate possible future enhancements.

If you are interested in delving further into the /proc file system, take a look at the Kernel Guide at the Linux Documentation Project (http://www.linuxdoc.org/LDP/tk/tk.html). Even without a background in operating systems, you may find this an interesting and enlightening read. To get the most out of it, you should have some familiarity with data structures in C.

## APPENDIX A

### Programming Languages that Accompany Red Hat Linux

Some of the programming languages that accompany Red Hat Linux are described in this appendix.

### The C/C++ Programming Suite

Red Hat Linux comes with the egcs compiler tools that provide a complete C and C++ programming suite. They include the compilers (gcc/g++), preprocessors (cpp), and debugger (gdb/xgdb). The compilers come with a complete set of header files and libraries, including an implementation of the STL library. Migrating code from other C compilers to gcc is reasonably straightforward. Migrating older code from C and C++ compilers to g++ is not quite as clean, mostly due to continuing disagreements over the C++ standards. The official C++ standard was established at the end of 1998, so we should hopefully see an easier transition path soon.

The closest thing to a fully integrated development environment that works with the C and C++ compilers is the Emacs editor. The Vim (VI Improved) editor is also a popular choice for C/C++ development.

> NOTE: Objective C is also supported using the egcs compiler suite; however, it is mainly used on systems running the NEXTSTEP operating system.

### GNU Fortran 77

Part of the egcs programming suite is the g77 compiler that implements Fortran 77. If you need this tool, you should be sure that the egcs C/C++ development tools are installed, too, since they share a common backend optimizer and code generator.

![](img/95b125a8bf06051f34d8aba73558b7eb_541_0.png)

### An Historical Aside

GNU Fortran 77 started in the mid-1980s as part of the Free Software Foundation's (FSF) GNU Project. FSF championed the project through the 1990s; however, as time went on, the rate at which bugs were fixed and new features were added to the compiler slowed down. This frustrated a group of developers who were fixing bugs and writing new features, only to find their work sitting on the sidelines, waiting for the maintainers to integrate them into the main distribution. Fed up, this group of programmers took the base source code, applied all of their changes, and released the updates under the name "egcs." Realizing that the egcs package was better for the free software movement, FSF decided to bless it as the official GNU C/C++ compiler in April 1999. Without the great work from both teams, we would not have the world-class compiler we have today.

### Tcl

Tcl is a multiplatform scripting language that is relatively easy to learn. With built-in primitives for building graphical user interfaces, it is becoming increasingly popular for tool builders since it makes it easy to create easy-to-use front ends that work across UNIX, Windows, and Macintosh. For example, to write the infamous "Hello, World" program in Tcl, you would only need the following lines of code:

```tcl
button .b -text 'Hello, World!' -command exit
pack .b
```

Tcl is also object oriented and easily extensible. See http://www.tcltk.com and http://www.telconsortium.org for more information.

### Expect

A derivative of Tcl, Expect is a scripting language geared towards automating other applications, such as tclnet and ftp. It essentially allows you to have the script send certain inputs to the application upon seeing certain outputs. If you're used to some of the scripting tools that come with terminal emulation packages like ProComm or Telix, you should feel right at home with Expect. And because it has the full power of Tcl behind it, you can perform some very interesting feats, given a little creativity. You must have Tcl installed to use Expect.

### ITcl

An extension to Tcl, ITcl offers an impressive array of object-oriented functionality to the base Tcl language, such as local name spaces and true inheritance. Developers writing programs longer than a few thousand lines in Tcl will most likely find ITcl to be a very useful addition. You must have Tcl installed to use ITcl.

### TclX

TclX is a series of extensions to the Tcl language that makes it easier to access files, perform network operations, debug code, and perform higher level math functions. You must have Tcl installed to use TclX.

### Tk

The Tk Widget Set is a series of widgets that makes it even easier to write GUIs that work in the UNIX, Windows, and Macintosh environments. The designer's goal is to provide an environment where writing GUIs takes only a little longer than writing text-based applications. You must have Tcl installed to use Tk.
