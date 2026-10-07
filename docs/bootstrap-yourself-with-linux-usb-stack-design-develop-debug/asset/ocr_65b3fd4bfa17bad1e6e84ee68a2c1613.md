# CHAPTER 18

# DEBUGGING USING LINUX USB

In This Chapter

+   - USB Monitor: usbmon
- Debug Using usbfs_snoop
- Verbose Debugging for Host-Side USB

For a developer, developing a system is simple, but debugging the same system to find the root cause of the problem requires extra ingenuity. This ingenuity can come from tools that can collect information on the system's state at the time of the problem. The complexity increases when the system to be debugged is part of a kernel subsystem. You can use many approaches to debug a kernel subsystem. Printing debug information in American Standard Code for Interchange (ASCII) text form is a common method developers use to debug modules in the kernel space. However, printing this information has limitations in terms of buffer size available. Also, sometimes an increase in information nullifies the problem.

So what does a protocol system such as universal serial bus (USB) need? In a protocol system, packet transfer detail is the key to debugging. Thus, details of USB transactions between a device and a host help isolate and fix the cause of a problem. Printing of so much information in ASCII text is not advisable from a practical standpoint. Moreover, it is difficult to print complete transaction information from low-level layers in any closed operating system.