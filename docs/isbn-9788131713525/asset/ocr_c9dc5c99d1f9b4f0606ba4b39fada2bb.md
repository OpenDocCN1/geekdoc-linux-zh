# 2.2.5 First User Space Process: init

One more important point should be made before moving on. Notice in Listing 2-3 this line:

```
INIT: version 2.78 booting.
```

Until this point, the kernel itself was executing code, performing the numerous initialization steps in a context known as *kernel context*. In this operational state, the kernel owns all system memory and operates with full authority over all system resources. The kernel has access to all physical memory and to all I/O subsystems.

When the Linux kernel has completed its internal initialization and mounted its root file system, the default behavior is to spawn an application program called *init*. When the kernel starts *init*, it is said to be running in *user space* or user space context. In this operational mode, the user space process has restricted access to the system and must use kernel system calls to request kernel services such as device and file I/O. These user space processes, or programs, operate in a virtual memory space picked at random⁴ and managed by the kernel. The kernel, in cooperation with specialized memory-management hardware in the processor, performs virtual-to-physical address translation for the user space process. The single biggest benefit of this architecture is that an error in one process can’t trash the memory space of another, which is a common pitfall in legacy embedded OSs and can lead to bugs that are difficult to track down.

Don’t be alarmed if these concepts seem foreign. The objective of this section is to paint a broad picture from which you will develop more detailed knowledge as you progress through the book. These and other concepts are covered in great detail in later chapters.

# 2.3 Storage Considerations

One of the most challenging aspects of embedded systems is that most embedded systems have limited physical resources. Although the Pentium 4 machine on your desktop might have 180GB of hard drive space, it is not uncommon to find embedded systems with a fraction of that amount. In many cases, the hard drive is typically replaced by smaller and less expensive nonvolatile storage devices. Hard drives are bulky, have rotating parts, are sensitive to physical shock, and require

> ⁴ It’s not actually random, but for purposes of this discussion, it might as well be. This topic will be covered in more detail later.