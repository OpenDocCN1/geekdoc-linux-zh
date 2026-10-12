There are enough version-1 Linux machines to be impressive, but they are rare. For practical purposes, the major number is 2; no one is quite sure what change would be big enough to jump to Linux-3, but we might assume it would cease to promise Linux-2 compatibility.

The last number is the incremental patch number and changes with every update. The first important portion of the kernel version number is the middle digit, the “minor” number. Odd minor numbers denote “experimental” kernels, the testbed for developers to explore, add new code, and bounce ideas off each other. Even minors, on the other hand, carry a stamp of respectability as “production editions.”

When a development kernel is ready, it follows the usual process of a feature freeze, then a code freeze, and is then promoted to the next even number. Thus, 2.3.99 became 2.4.0 and was simultaneously branched to become the new development 2.5 source. The road goes ever on.

![](bbox=[0.08, 0.42, 0.92, 0.46])

During the rapid development of the odd-minor kernels, you cannot simply jump in and expect to join the other kernel surfers. Although developers try to only release stable code, very often a core change can create havoc for other users. These troubles may be traced to upgraded libraries, modules, or compiler tools, but sometimes it is just a broken system and the development kernel can strand whole communities of users. Always check the Linux Kernel Web site (http://www.tux.org) or watch the "linux-kernel" mailing list. If your hardware is not flagged in the trouble reports, pick a development kernel revision that has been stable for at least a few days, and dive in.

# ## Obtaining the Kernel Sources

Every Linux distribution contains kernel sources. Red Hat offers install options to include the kernel headers, and a separate RPM to include the kernel sources. You must install the kernel headers if you plan to compile any software; to build the kernel, you must also install the kernel-sources RPM, or obtain kernel sources from some other source.

When fetching kernel sources, it is good netiquette to seek a mirror site as close to you as possible. Although famous sites such as Red Hat (ftp://ftp.redhat.com) and kernel.org (ftp://ftp.kernel.org/pub/linux) will have the files you need, you should check http://www.kernel.org for an appropriate mirror site.