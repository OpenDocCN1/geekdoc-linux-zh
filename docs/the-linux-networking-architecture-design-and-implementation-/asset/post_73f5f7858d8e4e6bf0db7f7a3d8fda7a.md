
## 2.4 Kernel Modules

by modprobe the configuration file. To be able to pass parameters to a module, you have to have previously declared these parameters in the module's source text. The following macros are available for this purpose:

- MODULE_PARM(var, type) designates the variable var as a parameter of the module, and a value can be assigned to this parameter during loading. It needs to be previously declared, of course. The second parameter of the macro (type) specifies the data type of the module parameter. The following types can be specified:
  - b: byte
  - h: short (two bytes)
  - i: integer
  - l: long
  - s: string (or a pointer to string)

If the parameter is an array, this can be specified by stating the array size before the type. For example, 1–31 means that the parameter is an array with integer values, and between one and three values can be assigned to this array. More information about this topic are included in the header file <linux/module.h>.

MODULE_PARM_DESC(var, desc) allows you to add a description (desc) for the parameter var. For example, this description is displayed when the tool modinfo is called. The description of a parameter should be short, but descriptive enough to make clear the task of that parameter.

In addition, the following macros can be used to output additional information, by the command-line tool modinfo. It is recommended that one use this informative option, because there could be situations where the user of a module does not provide the source text:

- MODULE_AUTHOR(name) can be used to specify the author of a module. It is recommended to also state an e-mail address, in addition to names, for easy contact in the event that the module contains errors (and, of course, to be able to accept the large number of thank-you messages for your generous contribution to the open-source movement :-).
- MODULE_DESCRIPTION(desc) should contain a description of the module's functionality. Ideally, describe the basic functionality and include reference to further information (e.g., a URL).
- MODULE_SUPPORTED_DEVICE(dev) is currently not used. However, it might be used in future kernel versions to load the module automatically when the device is required.

The sample module in Appendix D shows how to use the macros described above.

## 2.4.4 Symbol Tables of the Kernel and Modules

Kernel modules are object code, which is added to the kernel at runtime. Once it has been embedded, the module is in the kernel address space. Before the embedding of a module, however, several aspects have to be observed. As the module will probably have to call functions of actual kernel and use its data structures, we first have to resolve the addresses of these functions and data structures. The Linux kernel includes a table, the ksym symbol table; for this purpose this table includes all required information. Each row of the table contains the name and memory address of a function or variable. Information about the data type or parameters is not saved to the table. Note that the programmer has to ensure correct mapping.

You can see in Figure 2-6 that a module can access only functions and data stored in the kernel's symbol table. Other parts of the kernel are not accessible to a module. This has the benefit that modules communicate with the kernel exclusively over defined interfaces, as is true for the microkernel architectures described in Section 2.1.

The instruction EXPORT_SYMBOL (xxx) from the file kernel/ksym.c adds a function or variable of the kernel to the symbol table. From then on, each module can access these variables or call functions. In addition, modules can export references to functions and variables from the module into the symbol table. The macro EXPORT_SYMBOL can be used to allow modules to export selected function and data pointers into the symbol table of the kernel. A module that does not want to export methods or variables can simply use the EXPORT_NO_SYMBOLS to express its wish.

A module can normally access only those symbols that are listed in the symbol table when the module loads. For this reason, a situation where two modules loaded consecutively into the kernel want to access each other's symbols may cause problems. The module loaded first cannot access the symbols of the second module, because they are not yet known. Since Linux kernel Version 2.4, however, there is a solution to this problem. This solution is called intermediate communication and is introduced in [RuCo01] and [BBDK01].

> You can use the command-line call ksym to view the contents of the current symbol table.

## 2.5 Device Drivers

UNIX has its own way of handling physical devices. Device drivers in the form of modules can be added or removed in Linux at any time. Figure 2-7 shows an excerpt from the /dev directory, where all devices are listed. In Linux, network adapters are not treated as normal devices and are not listed in the /dev directory. Linux has a separate interface for them. The reasons are described in [RuCo01]. Chapter 5 will discuss network devices in detail.

The major number identifies the driver of a device. For example, Figure 2-7 shows that the PS/2 driver has major number 10 and the hard disk driver (hdx) has major number 3. The major number can be specified when you register a driver, but for drivers you will use less often, it is recommended that you let the kernel assign a major number. This ensures that the numbers are all unique. See details in [RuCo01].

The minor number is used to distinguish different devices used by the same driver and limiting their functionality. For example, an application programmer can use the simple file operations read() and write() to access the driver's hardware, where the ioctl() command can be used to configure properties of a device. In Linux, a device driver can control more than one device, if the driver is designed as reentrant. The minor number is used as an additional number to distinguish the devices that driver controls. For example, the hard disk driver with major number 3 in Figure 2-7 controls three hard disks, distinguished by minor numbers 1, 2, and 6. Figure 2-7 also shows that the type of each driver is specified at the beginning of each row. Linux differs between two types of physical devices:

Block-oriented devices allow optional access (i.e., an arbitrary set of blocks can be read or written consecutively without paying attention to the order). To increase performance, Linux uses a cache memory to access block devices. File system can be accommodated only in block devices (hard disks, CD-ROMs, etc.), because they are required for random access. Block devices are marked with a b in the /dev directory.

A block-oriented driver can be registered with the kernel function register_blkdev(). If the function called successfully, then the driver can be addressed by the returned major number. Release_blkdev() is used to release the device.

Character-oriented devices are normally accessed in sequential order. They can be accessed only outside of a cache. Most devices in a computer are character-oriented (e.g., printer and sound card). Character-oriented devices are marked with a c in the /dev directory. You can use register_chrdev() to register and release_chrdev() to release character-oriented devices.

The virtual file /proc/devices lists all devices currently known to the kernel. This file is used to find the major number of a driver in the user address space, in case none has been specified during the registration.

To be able to use a device that has not been registered yet, you need to first select a driver and generate an entry in the /dev directory. To create this entry, you use the command mknod /dev/name type major minor, which is passed the name, the type (block or character), the major number of the driver, and the selected minor number for that device. If the command is successful, then you can now use the file operations (read(), write(), ioctl(), ...) to access device.

Figure 2-8 shows how the data structure is passed when you register a character-oriented driver. A driver is addressed over a virtual file in UNIX so these are all regular file operations. We will briefly describe here only the most important functions, to give you an overview:

owner refers to the module implemented by the driver (for a module-based driver): lseek() sets the position pointer in a file. This function can be used for other purposes for non-oriented devices:

```
struct file_operations {
    struct module *owner;
    int (*lseek) (file, offset, origin);
    int (*read) (file, buffer, count, pos);
    int (*write) (file, buffer, count, pos);
    int (*readdr) (file, dir);
    int (*poll) (file, poll_table);
    int (*ioctl) (inode, file, cmd, unsigned arg);

    int (*open) (inode, file);
    int (*release) (inode, file);
}
```
