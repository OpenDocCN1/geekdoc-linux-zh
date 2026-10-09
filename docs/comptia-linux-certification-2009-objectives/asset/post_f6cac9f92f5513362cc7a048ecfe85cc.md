
## Kernel Layer
| Kernel Layer | Function |
| :--- | :--- |
| *Device management* | A layer in the kernel that manages devices by controlling device access and interfacing between user applications and hardware devices of the computer. |
|  | When the user application sends a system call, the kernel reads the request and passes it on to the drivers that manage the activities of that particular device. For this purpose, the kernel maintains a list of devices in the `/dev` directory. |

### Types of Kernels
Kernels can be classified as monolithic and modular, based on their organization.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_314_0.png)

| Kernel Type | Description |
| :--- | :--- |
| *Monolithic* | In a monolithic kernel, all modules, such as device drivers or filesystems, are built-in. |
|  | Monolithic kernels can interact faster with devices. But the major disadvantage is its huge size, which leads to higher usage of RAM. |
| *Modular* | In a modular kernel, only a minimal set of essential modules are built-in. The rest of the modules can be installed and the kernel can be rebuilt whenever necessary. A modular kernel is also known as a micro kernel or a dynamic kernel. |
|  | Modular kernels are flexible and save memory usage because the kernel modules, which are loaded as required, are removed from the memory when the related devices are unmounted. |

## ACTIVITY 8-1
### Exploring the Role and Functions of the Linux Kernel

**Scenario:**
As a system administrator, you may need to troubleshoot issues related to the kernel. So, you will like to explore the kernel concepts to refresh your knowledge.

1. Which function is associated with the SCI layer of the kernel?
   a) Passing requests to device drivers
   b) Sending service requests to the kernel
   c) Processor time allocation for functions
   d) Process scheduling functions
   e) File organization

2. What are the major functions performed by the kernel? Select all that apply.
   a) Kernel initialization
   b) Process management
   c) Memory management
   d) Module installation
   e) Dependency management

3. True or False? The kernel maintains a list of all devices in the /boot directory.
   - [ ] True
   - [x] False

## TOPIC B
### Customize Kernel Modules
You familiarized yourself with the basic concepts of the Linux kernel. Kernel modules are functions that extend the capability of the kernel to support additional functionalities. In this topic, you will customize kernel modules.

The Linux kernel, by default, loads with a minimum set of kernel modules. When you want the kernel to support some additional functionalities, you have to install or load the necessary modules manually. Customizing the modules to suit user requirements will enable you to manage the kernel efficiently.

### Kernel Modules
![](img/477ccb2f05b6ba1b2d563ea74f18c197_316_0.png)

**Definition:**
*A kernel module* is a system-level function that extends the functionality of the kernel. It can be dynamically loaded into the kernel or unloaded from the kernel when required. It enables the kernel to update or recompile itself without requiring the system to reboot. The kernel module file consists of a .ko extension. The modules built for a specific kernel version may not be compatible with another version of the kernel.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_316_1.png)

#### Advantages of Kernel Modules
The advantages of kernel modules are:

- Kernel modules reduce the burden on the kernel. If kernel modules were not present, their functionalities have to be added directly to the kernel image, which can make the kernels larger.
- Kernel modules avoid rebuilding and rebooting of the system when a new functionality is required.
- Dynamic loading of kernel modules facilitate lower memory consumption.

### Directories Containing Kernel Modules
The /lib/modules directory contains the modules of different kernel versions that are installed. It contains a directory named after the kernel's version number. A list of currently loaded modules is found in the /proc/modules file. Modules are stored across various directories based on the categories they belong to. The following table lists the directories containing modules.

| Directories | Description |
| :--- | :--- |
| pcmcia | Contains modules for PCMCIA (PC card). |
| net | Contains modules for network-related products such as firewalls and protocols. |
| drivers | Contains modules for various types of hardware. |
| fs | Contains modules for various types of filesystems. |
| arch | Contains modules for architecture specific support. |

![](img/477ccb2f05b6ba1b2d563ea74f18c197_317_0.png)

### Kernel Module Managing Utilities
A kernel module managing utility enables you to view, load, unload, or modify kernel modules.

| Kernel Module Utility | Enables You To |
| :--- | :--- |
| lsmod | Display the currently loaded kernel modules, their size, usage details, and their dependent modules. |
| modinfo | Display information about a particular kernel module such as file name of the module, license, description, author's name, module version number, dependent modules, and other parameters or attributes. The syntax of this command is `modinfo (module options)`. |
| insmod | Install a module into the currently running kernel. This utility inserts only the specified module and does not insert any dependent modules. The syntax of this command is `insmod (file name) (module options)`. |
| modprobe | Add or remove modules from a kernel. This utility is capable of loading all dependent modules before inserting a specified module.<br>- The syntax for adding a module is: `modprobe (module name)`.<br>- The syntax for removing a module is: `modprobe -r (module name)`. |

### Command Options for modinfo
The command options for the modinfo command are listed in the table below.

| Command Option | Enables You To |
| :--- | :--- |
| -v | Display the version number of the modinfo utility. |
| -n | Display the file name of the module. |
| -a | Display the author of the module. |
| -d | Display the description about the module. |
| -P | Display the parameters supported by the module. |
| -F | Print the field values, such as parameters, author, and description. |

### Command Options for insmod
The command options for the insmod command are listed in the table below.

| Command Option | Enables You To |
| :--- | :--- |
| -e | Add persistent parameters for the module. |
| -f | Force the loading of a module even when there is a difference between the module's kernel version and the current kernel version. |
| -L | Prevent simultaneous loading of the same module. |
| -o (module name) | Specify a module name while installing the module. |

### Command Options for modprobe
The command options for the modprobe command are listed in the table below.

| Command Option | Enables You To |
| :--- | :--- |
| -a | Add all modules specified in the command line. |
| -r | Remove all modules specified in the command line. |
| -v | Display the verbose of all commands when they are executed. |
| -1 | List all modules that match the given wildcard information. |
| -t (directory name) | List all modules present in a specified directory. |

![](img/477ccb2f05b6ba1b2d563ea74f18c197_319_0.png)

### The modprobe.conf File
The modprobe.conf file is a configuration file, which contains settings that apply persistently to all modules loaded on the system. It is used to configure modules and their dependencies and also specify module aliases.

> The /etc/modules.conf file was used to manage kernel modules in older versions of Linux.

The modprobe.conf file, which is located in the /etc/modprobe.d directory, has a number of options for configuring kernel modules.

| Option | Used To |
| :--- | :--- |
| `alias wildcard module name` | Specify an alternate name for a module with a long name. |
| `include file name` | Add configuration files to the module. |
| `options module name option` | Specify the options to be added to each module before insertion into the kernel. |
| `install module name command` | Run the command specified without inserting the module into the kernel. |

![](img/477ccb2f05b6ba1b2d563ea74f18c197_319_1.png)

*Figure 8-3: The modprobe.conf file is used to configure the kernel modules.*
