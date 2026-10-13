# Modules

The Linux kernel employs the use of modules to support different operating system features, including support for various devices such as sound and network cards. In many cases, you do have the option of implementing support for a device either as a module or by directly compiling it as a built-in kernel feature, which requires you to rebuild the kernel (see Chapter 33). A safer and more robust solution is to use modules. Modules are components of the Linux kernel that can be loaded as needed. To add support for a new device, you can now simply instruct a kernel to load the module for that device. In some cases, you may have to recompile only that module to provide support for your device. The use of modules has the added advantage of reducing the size of the kernel program as well as making your system more stable. The kernel can load modules in memory only as they are needed. Should a module fail, only the module stops running, and it will not affect the entire system. For example, the module for the PPP network interface used for a modem needs to be used only when you connect to an ISP.

# Kernel Module Tools

The modules your system needs are usually determined during installation, based on the kind of configuration information you provided and the automatic detection performed by Kudzu. For example, if your system uses an Ethernet card whose type you specified during installation, the system loads the module for that card. You can, however, manually control what modules are to be loaded for your system. In effect, this enables you to customize your kernel whatever way you want. You can use several commands, configuration tools, and daemons to manage kernel modules. The 2.4 Linux kernel includes the Kernel Module Loader (Kmod), which has the capability to load modules automatically as they are needed. Kernel module loading support must also be enabled in the kernel, though this is usually considered part of a standard configuration and is included with Red Hat distributions. In addition, several tools enable you to load and unload modules manually, if you must. The Kernel Module Loader uses certain kernel commands to perform the task of loading or unloading modules. The modprobe command is a general-purpose command that calls insmod to load modules and rmmod to unload them. These commands are listed in Table 32-5. Options for particular modules, general configuration, and even specific module loading can be specified in the /etc/modules.conf file. You can use this file to automatically load and configure modules. You can also specify modules to be loaded at the boot prompt or in grub.conf (see Chapter 27).

Table 32-4: Video Devices

| Device Name | Type of Device |
|---|---|
| /dev/video | Video capture interface |
| /dev/vfx | Video effects interface |
| /dev/codec | Video codec interface |
| /dev/vout | Video output interface |
| /dev/radio | AM/FM radio devices |
| /dev/vtx | Teletext interface chips |
| /dev/vbi | Data services interface |

# Module Files and Directories

The filename for a module has the extension .o. Kernel modules reside in the /lib/modules/version directory, where version is the version number for your current kernel. The directory for the 2.4.22-1 kernel is /lib/modules/2.4.22-1. As you install new kernels on your system, new module directories are generated for them. One method to access the directory for the current kernel is to use the uname -r command to generate the kernel version number. This command needs to have backquotes.

```
cd /lib/modules/`uname -r`
```