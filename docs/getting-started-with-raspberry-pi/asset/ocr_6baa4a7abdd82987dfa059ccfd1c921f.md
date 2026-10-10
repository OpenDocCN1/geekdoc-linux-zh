# # Tracing

Tracing provides insight into behavioral problems that manifest during interactions between different code modules. A common way to obtain execution traces is by using `printk`. While `printk` is perhaps the most heavily used method for kernel debugging (there are more than 62,000 `printk()` statements in the 2.6.23 source tree), it is not sophisticated enough for high-volume tracing. *Linux Trace Toolkit* (LTT) is a powerful tool that lets you obtain complex system level traces with minimum overhead.

# ## Linux Trace Toolkit

LTT extracts execution traces that are useful for postmortem analysis and is valuable in situations where it may not be possible to use a debugger. Unlike OProfile, which collects data by sampling events at regular intervals, LTT provides exact traces of events as and when they occur.

LTT consists of four components:

+   • A core module that provides trace services to the rest of the kernel. The collected traces are copied to a kernel buffer.

+   • Code that makes use of the trace services. These are inserted at points where you want to capture trace dumps.

+   • A trace daemon that pulls trace information from the kernel buffer to a permanent location in the filesystem.

+   • Utilities such as `tracereader` and `tracevisualizer` that interpret raw trace data and convert it into human-readable form. If you are developing code for an embedded device having no GUI support, you can transparently run these tools on another machine.

LTT is not part of the mainline kernel.[8] You may download LTT kernel patches, trace daemon, and user-space trace utilities from www.opensys.com/LTT.

> [8] LTT was included as a release candidate in the 2.6.11-rc1-mm1 patch, downloadable from www.kernel.org.

Let's find out what LTT offers with the help of a simple example. Assume that you are seeing data corruption when your application is reading from a device. You first want to figure out whether the device is sending bad data or whether a kernel layer is introducing the corruption. To do that, dump data packets and data structures at the device driver level. Listing 21.7 initializes the LTT events that you plan to generate.

**Listing 21.7. Creating LTT Events**