# 2.6 Memory Management in the Kernel 31

read() transfers data from the driver to the user address space. The driver has have previously confirmed that the desired buffer is available in the user address space and whether this memory page is currently outsourced. Subsequently, the function copy_to_user() can be used to copy data to the user address space.

As with read(), write() is used to transfer data, in this case, from the user address space to the kernel address space (with copy_from_user()). Here again, before you can copy, you have to check the validity of the range in the user address space. The memory range in the kernel does not have to be verified, because the kernel segment is never outsourced.

ioctl() offers the most extensivity. It is used to set certain parameters of a driver or device. A constant that represents the desired "command" and a pointer to the data to be passed with this command are passed to the ioctl() command. This can be arbitrary data. The power of this function is that the ioctl() command could actually replace all other file operations of a driver.

open() and close() are used to prepare (or postedit) a device for subsequent (or completed) commands. This function must not be confused with similar functions to configure a driver. Such tasks are normally executed by the ioctl() command. open() is called by a process to inform the driver that it wants to use the device. If a process can be made available only exclusively, open() checks on another process has already opened that device, and if so, denies access to it.

close() releases the device. Whether exclusive use is desired depends on the type of device.

When a device is accessed, certain things can happen at the interface of the device driver. For example, if you use the C library fopen() to open a device file from the /dev directory, then the open() function of the device file is called in the kernel. If you use fprint() to write data to the device file, then the write() function of the driver will run in the kernel. Not all operations of a driver have to be supported; only those that the driver really needs.

# 2.6 MEMORY MANAGEMENT IN THE KERNEL

Memory management is one of the main components in the kernel of any operating system. It supplies a virtual memory space to processes, often much larger than the physical memory. This can be achieved by partitioning memory pages and outsourcing memory pages that are temporarily not needed to the swap memory on the hard disk. Access to an outsourced page by an application is intercepted and handled by the kernel. The page is reloaded into the physical memory and the application can access the memory without noticing anything about insourcing or outsourcing of things.

The memory residing in the kernel cannot be outsourced because, if the memory management were to move the code to the swap memory, it would not be available later

> The commands and their constants are specified arbitrarily by the programmer, but they should be unique within the kernel. For this reason, it is recommended to use a hierarchical coding. (See RuCo01).