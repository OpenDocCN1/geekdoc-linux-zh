```
5
6    #define lock kernel()                       do { } while(0)
7    #define unlock kernel()                     do { } while(0)
8    #define release kernel lock(task, cpu)       do { } while(0)
9    #define reacquire kernel lock(task)          do { } while(0)
10
11
12
13     #include <asm/smplock.h>
14
15     #endif /* __SMP__ */
16
17     #endif
18
```

# ## Device Handling

All device handling within the Linux kernel happens through *special files*. A special file appears in the file system tree structure as a normal file under `/dev`. These special files, however, use no space. Rather, these special files are links to device drivers. The device drivers are either included within the kernel or else called on demand by means of the kernel modules mechanism. It is usually up to the system administrator to decide whether to compile a driver into the kernel or make it a loadable module. Having a driver compiled inside the kernel slightly increases the size of the kernel binary image until it might not fit onto a single diskette. Using loadable modules, however, increases response time for the first-ever access to the device, because the kernel must first locate the module and append it to itself.

Because this book addresses servers rather than smaller installations, the issue of having a slightly bigger kernel is not considered. It is unheard of for a server to boot from diskettes, except for testing and/or kernel-maintenance tasks. Adding a few kilobytes to a kernel is not a cause of concern. On a machine with 1GB of memory, the kernel easily takes up to 50MB for the complete complement of kernel structures, as we will see later.

When a process opens a special file, the kernel redirects all read and write requests to the appropriate device driver. The driver in turn executes the original read or write operation on behalf of the process. There are two types of special files, the *block mode device* and the *character mode device*. All such devices share the same meta-information:

+   - Type (block or character).