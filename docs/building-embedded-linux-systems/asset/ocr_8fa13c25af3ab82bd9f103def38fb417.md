Since Modbus specifies a messaging structure, it is independent of the underlying physical layer. There are two formats used to transmit information with Modbus: ASCII and RTU. The first sends each byte as two ASCII characters, whereas the second sends each byte as two 4-bit hexadecimal characters. Modbus is usually implemented on top of a serial interface such as RS232, RS422, or RS485. In addition to Modbus, Schneider specifies the Modbus TCP/IP protocol, which uses TCP/IP and Ethernet to transmit Modbus messages.

Three open source projects provide Modbus capabilities to Linux:

+   - *jModbus*
+     This project aims to provide a Java implementation of Modbus RTU, Modbus ASCII, and Modbus TCP/IP. It resides at http://jmodbus.sourceforge.net and is distributed with documentation and examples under a BSD-style license.

+   - *libmodbus*
+     This is an active, up-to-date project that develops a C-based shared library for use in applications. Several existing projects use it, and it has the usual array of online Bazaar-based source versioning<sup>†</sup> and the like. It is licensed under version 3.0 of the GPL and is available at http://copyleft.free.fr/wordpress/index.php/libmodbus.

+   - *MAT LinuxPLC*
+     This is the same automation project mentioned earlier in “I/O.” The MAT project now contains code implementing Modbus RTU and Modbus TCP/IP in its CVS repository. Although the source code is commented, there is little other documentation.

For more information about Modbus, read the Modbus specifications, available at http://www.modbus.org.

# System Monitoring

Both hardware and software are prone to failure, sometimes drastically. Although the occurrence of failures can be reduced through careful design and runtime testing, they are sometimes unavoidable. It is the risk of the embedded system designer to plan for such a possibility and to provide means of recovery. Often, failure detection and recovery is done by means of system monitoring hardware and software such as *watchdogs*.

Linux supports two types of system monitoring facilities: watchdog timers and hardware health monitoring. There are both hardware and software implementations of watchdog timers, whereas health monitors always require appropriate hardware. Watchdog timers depend on periodic reinitialization so as not to reboot the system. If the system hangs, the timer eventually expires and causes a reboot. Hardware health

> † Bazaar is a software configuration management tool originally used by the Ubuntu project, an implementation and a fork of GNU Arch.