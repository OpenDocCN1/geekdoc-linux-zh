# 44 Chapter 5. The proc File System

When viewing different virtual files in the /proc/ file system, some of the information is easily understandable while some is human-readable. This is in part why utilities exist to pull data from virtual files and display it in a useful way. Examples of these utilities include lspci, apm, free, and top.

> Note
Some of the virtual files in the /proc/ directory are readable only by the root user.

# 5.1.2. Changing Virtual Files

As a general rule, most virtual files within the /proc/ directory are read only. However, some can be used to adjust settings in the kernel. This is especially true for files in the /proc/sys/ subdirectory.
To change the value of a virtual file, use the echo command and a > symbol to redirect the new value to the file. For example, to change the hostname on the flly:

```
echo www.example.com > /proc/sys/kernel/hostname
```

Other files act as binary or boolean switches. Typing Cat /proc/sys/net/ipv4/ip_forward returns either 0 or a 1 indicates that the kernel is not forwarding network packets. Using the echo command to change the value of the ip_forward file to 1 immediately turns packet forwarding on.

> Tip
Another command used to alter settings in the /proc/sys/ subdirectory is /sbin/sysctl. For more information on this command, see Section 5.4 Using the sysctl Command

For a listing of some of the kernel configuration files available in the /proc/sys/, see Section 5.3.9 /proc/sys/

# 5.2. Top-level Files in the proc File System

Below is a list of some of the more useful virtual files in the top-level of the /proc/ directory.

> Note
In most cases, the content of the files listed in this section will not be the same on your machine. This is because much of the information is specific to the hardware on which Red Hat Linux is running.