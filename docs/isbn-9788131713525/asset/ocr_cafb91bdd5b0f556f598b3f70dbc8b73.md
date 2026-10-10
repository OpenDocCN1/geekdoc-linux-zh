# 15.6 Chapter Summary

+   - Remote (cross) debugging enables symbolic debugging using host development workstation resources for the heavy lifting, preserving often scarce target resources.

+   - gdbserver runs on the target system and acts as the glue between the cross-gdb running on a development host and the process being debugged on the target.

+   - GDB on the host typically uses IP connections via Ethernet to send and receive commands to gdbserver running on the target. The GDB remote serial protocol is used between GDB and gdbserver.

+   - GDB can halt on shared library events and can automatically load shared library symbols when available. Your toolchain should be configured for the default paths on your cross-development system. Alternatively, you can use GDB commands to set the search paths for shared library objects.

+   - GDB can be used to debug multiple independent processes via multiple concurrent GDB sessions.

+   - GDB can be configured to follow a forked process on a fork() system call. Its default mode is to continue to debug the parent—that is, the caller of fork().

+   - GDB has features to facilitate debugging multithreaded applications written to POSIX thread APIs. The current default Linux thread library is the Native Posix Threads Library (NPTL).

+   - GDB supports attaching to and detaching from an already running process.

# 15.6.1 Suggestions for Additional Reading

GDB: The GNU Project Debugger
Online Documentation
http://sourceware.org/gdb/onlinedocs/

*GDB Pocket Reference*
Arnold Robbins
O’Reilly Media, 2005