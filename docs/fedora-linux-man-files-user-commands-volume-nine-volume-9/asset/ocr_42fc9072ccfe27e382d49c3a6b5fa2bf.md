already exist, and overwritten if it does. **path** is required.

**-chardev pipe ,id=id ,path=path** Create a two-way connection to the guest. The behaviour differs slightly between Windows hosts and other hosts:

On Windows, a single duplex pipe will be created at `\.pipe\path`.

On other hosts, 2 pipes will be created called *path.in* and *path.out*. Data written to *path.in* will be received by the guest. Data written by the guest can be read from *path.out*. **QEMU** will not create these fifos, and requires them to be present.

**path** forms part of the pipe path as described above. **path** is required.

**-chardev console ,id=id** Send traffic from the guest to **QEMU**'s standard output. **console** does not take any options.

**console** is only available on Windows hosts.

**-chardev serial ,id=id ,path=path** Send traffic from the guest to a serial device on the host.

On Unix hosts serial will actually accept any tty device, not only serial lines.

**path** specifies the na of the serial device to open.

**-chardev pty ,id=id** Create a new pseudo-terminal on the host and connect to it. **pty** does not take any options.

**pty** is not available on Windows hosts.

**-chardev stdio ,id=id [ ,signal=on|off]** Connect to standard input and standard output of the **QEMU** process.

**signal** controls if signals are enabled on the terminal, that includes exiting **QEMU** with the key sequence **Control-c**. This option is enabled by default, use **signal=off** to disable it.

**stdio** is not available on Windows hosts.

**-chardev braille ,id=id** Connect to a local BrLAPI server. **braille** does not take any options.

**-chardev tty ,id=id ,path=path** **tty** is only available on Linux, Sun, FreeBSD, NetBSD, OpenBSD and DragonFlyBSD hosts. It is an alias for **serial**.

**path** specifies the path to the tty. **path** is required.

**-chardev parallel ,id=id ,path=path** **-chardev parport ,id=id ,path=path** **parallel** is only available on Linux, FreeBSD and DragonFlyBSD hosts.

Connect to a local parallel port.

**path** specifies the path to the parallel port device. **path** is required.

**-chardev spicevmc ,id=id ,debug=debug ,na=na** **spicevmc** is only available when spice support is built in.

**debug** debug level for spicevmc

**na** na of spice channel to connect to