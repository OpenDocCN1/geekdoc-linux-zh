
# Managing Modules

When using a modular kernel, special tools are required to manage the modules. Modules must be loaded and unloaded and it would be nice if that were done automatically as much as possible. We also need to be able to pass necessary parameters to modules when we load them—things as memory addresses and interrupts. (That information varies from module to module, so you'll need to look at the documentation for your modules to determine what, if any, information needs to be passed to.) In this section, we'll cover the tools provided to manage modules and then look at a few examples of using them.

Linux provides the following module management tools for our use. All these commands (and modules.conf) have many pages:

- lsmod—This command lists the loaded modules. It is useful to pipe this through the less command because the listing is usually more than one page long.

- insmod—This command loads the module into the running kernel. If a module name is given without a full path, the default location for the running kernel, /lib/modules/*, will be searched. Several options are offered for this command—the most useful is -f, which forces the module to be loaded.

- rmmod—This command unloads (removes) the specified module from the running kernel. More than one module at a time can be specified.

- modprobe—A more sophisticated version of insmod and rmod, it uses the dependency file created by depmod and automatically handles loading, or with the -r option, removing modules. There is no force option, however. A useful option for modprobe is -t. If you were unsure of what module would work for your network card, you could use this command:

```
# modprobe -t net
```

The term net is used because it is the name of the directory (/lib/modules/*/kernel/net) where all the network drivers are kept. It will try each one in turn until it loads successfully.

- depmod—This program creates a dependency file for kernel modules. Some modules need to have other modules loaded first; that is they “depend” on the other modules. (A lot of the kernel code is like this it eliminates redundancy in the code base.) During the boot process, one of the startup files contains the command depmod -a and it runs every time you need to re-create the file /lib/modules/**/*.dep. If you make changes to the file /etc/modules.conf, run depmod -a manually. The depmod command, its list of dependencies, and the /etc/modules.conf file enable kernel modules to be automatically loaded as needed.

- /etc/modules.conf—This is not a command, but a file that controls how modprobe and depmod behave; it contains kernel variables. Although the syntax can be complex, most actual needs are very simple. The most common use is to alias a module and pass it to some parameters. For example, in the following code, we alias a device name (from devices.txt) to a more descriptive word and then pass some information to an associated module. the i2c-dev device is used to read the CPU temperature and fan speed on our system. These lines for /etc/modules.conf were suggested for our use by the program's documentation. We added them with a text editor.

```
alias char-major-89 i2c-dev
options eeprom ignore=2,0x50,2x051,2x052
```

A partial listing of lsmod is shown here, piped through the less command allowing us to view it at a time:

| Module | Size | Used by | Tainted |
| :--- | :--- | :--- | :--- |
| joydev | 5632 | 0 | (unused) |
| input | 3456 | 0 | [joydev] |
| lp | 6720 | 0 | (unused) |
| parport_pc | 21672 | 1 | |
| parport | 23936 | 1 | [lp parport_pc] |
| scanner | 9140 | 0 | |
| loop | 11376 | 6 | (autoclean) |

The list is actually much longer, but here we see that the input module is being used by the joydev (joystick device) module, but the joystick module is not being used. My computer has a joystick port that autodetected, but no joysticks connected. A scanner module is also loaded, but because the USB scanner is unplugged, the module is not being used. You would use the lsmod command to check if a module was loaded and what other modules were using it. If you examine the full list, you'd see modules for all the devices attached to this computer.

To remove a module, joydev in this example, use:

- rmmod joydev

A look at the output of lsmod would now show that it is no longer loaded. If we removed input as well, we could then use modprobe to load both input and joydev (one depends on the other, remember) with a simple:

- modprobe joydev

If Red Hat Linux refuses to boot at loading a module (because it had been compiled using different kernel version from what we are currently running; for example, the Nvidia graphics card module), we could force it to load this like:

- insmod -f NVdriver

We would ignore the complaints (error messages) in this case if the kernel generated any. (It won't.)

# CHAPTER 24 Kernel and Module Management

In Chapter 25, "Productivity Applications," you learn about loading a scanner module; in the example there, you manually load the scanner module and pass the vendor ID. The scanner was not included in the lookup list because it's not supported by the GPL scanner programs; as a result, the scanner module was not automatically detected and loaded. However, the scanner will work with a closed-source application after the module is loaded. Automatic module management is nice when it works, but sometimes it's necessary to work with modules directly.

# When to Recompile

Red Hat uses a modified version of the plain vanilla Linux kernel (a modified version is referred to as a patched kernel) with additional drivers and other special features compiled into it.

Red Hat has quite an intensive testing period for all distribution and regularly distributes updated versions. The supplied Red Hat kernel is compiled with as many modules as possible to provide as much flexibility as possible. A running kernel can be further tuned with sysctl scripts, which enables direct access to a running kernel and permits some kernel parameters to be changed (see the sysctl section at the end of the chapter). As a result of this extensive testing, configurability, and modularity, the precompiled Red Hat Linux kernel does everything users need it to do. Most users only need to recompile the kernel to:

- Accommodate an esoteric piece of hardware
- Conduct a system update when Red Hat has not yet provided precompiled kernels
- Experiment with the system capabilities

Red Hat supplies several precompiled versions of the kernel for Athlon and Pentium processors, for single- and multi-processor motherboards and for Enterprise-class systems. (Higher security ushers 4GB of memory:) These kernel versions are provided in RPM format and installing them is as easy as:

```
# rpm -Uvh newkernel.rpm
```

The kernel (but not the source) RPM files include installation scripts that will alter your bootloader configuration, making the kernel the default. If you don't want that to happen, manually edit the /etc/lilo.conf or /boot/grub/grub.conf files and change them back. You can obtain information on configuring both the LILO and GRUB bootloaders in Chapter 7.

> CAUTION
> You always rpm -U (upgrade), rather than rpm -i (install), a new kernel rpm to avoid overwriting the old, but still working kernel. This is done as a safety measure.

# Kernel Versions

Each new kernel has an associated kernel source RPM and it is installed with:

```
# rpm -Uvh newkernel.src.rpm
```

The source code is automatically installed to /usr/src.

# Kernel Versions

The Linux kernel is in a constant state of development. As new features are added, bugs are fixed, and new technology is incorporated into the code base, it becomes necessary to provide stable releases of the kernel for use in a production environment. It's also important to have separate releases that contain the newest code for developers. To keep track of the kernels, version numbers exist solely to differentiate and organize sequential revisions of software.

On the authors' test system, for example, the kernel version number is 2.4.19-7.80.

The kernel version can be broken down into four sections:

- major version—This is the major version number, now at 2. Think of this as volume 2 of a book.
- minor version—This is the minor version number, now at 4. Think of this as Chapter 4 in volume 2 of that book.
- sublevel number—This indicates the current iteration of the kernel; for our preceding example, it is at 19. Think of this as page 19 of Chapter 4, volume 2 in that book.
- extraversion level—This is the number representing a collection of patches and additions made to the kernel by the Red Hat engineers to make the kernel work for them (and you). Each collection is numbered, and the number is indicated here in the kernel name. From our preceding example, it is 7.80. Think of this as the 7.8th revision of page 19, Chapter 4, volume 2 in that book.

Typing uname -r at the command prompt displays your current kernel version.

```
# uname -r
2.4.18-7.80
```
