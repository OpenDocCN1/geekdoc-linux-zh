
# Video, TV, and DVD Devices

Device names used for TV, video, and DVD devices are listed in Table 32-4. Drivers for DVD and TV decoders have been developed. mg4linux (marvel.sourceforge.net) is developing video support for the Matrox Multimedia cards such as the Marvel G200. The General ATI TV and Overlay Software (GATOS) (gatos.sourceforge.net) has developed drivers for the currently unsupported features of ATI video cards, specifically TV features. The BTTV Driver Project has developed drivers for the Booktree video chip. Creative Labs sponsors Linux drivers for the Creative line of DVD DXR2 decoders (opensource.creative.com).

## Modules

The Linux kernel employs the use of modules to support different operating system features, including support for various devices such as sound and network cards. In many cases, you do have the option of implementing support for a device either as a module or by directly compiling it as a built-in kernel feature, which requires you to rebuild the kernel (see Chapter 33). A safer and more robust solution is to use modules. Modules are components of the Linux kernel that can be loaded as needed. To add support for a new device, you can now simply instruct a kernel to load the module for that device. In some cases, you may have to recompile only that module to provide support for your device. The use of modules has the added advantage of reducing the size of the kernel program as well as making your system more stable. The kernel can load modules in memory only as they are needed. Should a module fail, only the module stops running, and it will not affect the entire system. For example, the module for the PPP network interface used for a modem needs to be used only when you connect to an ISP.

## Kernel Module Tools

The modules your system needs are usually determined during installation, based on the kind of configuration information you provided and the automatic detection performed by Kudzu. For example, if your system uses an Ethernet card whose type you specified during installation, the system loads the module for that card. You can, however, manually control what modules are to be loaded for your system. In effect, this enables you to customize your kernel whatever way you want. You can use several commands, configuration tools, and daemons to manage kernel modules. The 2.4 Linux kernel includes the Kernel Module Loader (Kmod), which has the capability to load modules automatically as they are needed. Kernel module loading support must also be enabled in the kernel, though this is usually considered part of a standard configuration and is included with Red Hat distributions. In addition, several tools enable you to load and unload modules manually, if you must. The Kernel Module Loader uses certain kernel commands to perform the task of loading or unloading modules. The modprobe command is a general-purpose command that calls insmod to load modules and rmmod to unload them. These commands are listed in Table 32-5. Options for particular modules, general configuration, and even specific module loading can be specified in the /etc/modules.conf file. You can use this file to automatically load and configure modules. You can also specify modules to be loaded at the boot prompt or in grub.conf (see Chapter 27).

### TABLE 32-4
Video Devices

| Device Name | Type of Device |
|---|---|
| /dev/video | Video capture interface |
| /dev/vfx | Video effects interface |
| /dev/vdec | Video codec interface |
| /dev/vout | Video output interface |
| /dev/radio | AM/FM radio devices |
| /dev/vtx | Teletext interface chips |
| /dev/vbi | Data services interface |

## Module Files and Directories

The filename for a module has the extension .o. Kernel modules reside in the /lib/modules/version directory, where version is the version number for your current kernel. The directory for the 2.4.22-1 kernel is /lib/modules/2.4.22-1. As you install new kernels on your system, new module directories are generated for them. One method to access the directory for the current kernel is to use the uname -r command to generate the kernel version number. This command needs to have backquotes.

```
cd `/lib/modules/`uname -r`
```

In this directory, modules for the kernel reside in the /kernel directory. Within the /kernel directory are several subdirectories, including the /drivers directory that holds subdirectories for modules like the sound drivers or video drivers. These subdirectories serve to categorize your modules, making them easier to locate. For example, the kernel/drivers/net directory holds modules for your Ethernet cards, and the kernel/drivers/sound directory contains sound card modules.

### TABLE 32-5
Kernel Module Commands

| Command | Description |
|---|---|
| lsmod | Lists modules currently loaded. |
| insmod | Loads a module into the kernel. Does not check for dependencies. |
| rmmod | Unloads a module currently loaded. Does not check for dependencies. |
| modinfo | Display information about a module: -a (author), -d (description), -p (module parameters), -f (module filename), -v (module version). |
| depmod | Creates a dependency file listing all other modules on which the specified module may rely. |
| modprobe | Loads a module with any dependent modules it may also need. Uses the file of dependency listings generated by depmod: -r (unload a module), -l (list modules) |
