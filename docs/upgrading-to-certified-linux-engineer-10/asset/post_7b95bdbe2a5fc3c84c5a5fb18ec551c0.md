
## Manage Modules from the Command Line

The following are commands you can use from a command line when working with modules:

- **lsmod.** This command lists the currently loaded modules in the kernel.

  The following is an example:

  ```
DAS50:~ # lsmod
Module          Size  Used by
quota_v2        12928  2
edd             13720  0
joydev          14528  0
sg              41632  0
st              44956  0
sr_mod          21028  0
ide_cd          42628  0
cdrom           42780  2 sr_mod,ide_cd
nvram           13448  0
usbserial       35952  0
parport_pc      41024  1
lp              15364  0
parport         44232  2 parport_pc,lp
ipv6            275348  44
uhci_hcd        25728  0
intel_agp       22812  1
agpgart         36140  1 intel_agp
evdev           13952  0
usbcore         116572  4 usbserial,uhci_hcd
  ```

  The list includes information about the module name, size of the module, how often the module is used, and by which other modules use it.

- **insmod module.** This command loads the indicated *module* into the kernel.

  The module must be stored in the directory `/lib/modules/version_number/`. However, it is recommended to use modprobe for loading modules.

- **rmmod module.** This command removes the indicated *module* from the kernel. However, it can only be removed if no processes are accessing hardware connected to it or corresponding services.

  We recommend that you use `modprobe -r` for removing modules.

- **modprobe module.** This command loads the indicated *module* into the kernel or removes it (with option -r).

  Dependencies of other modules are taken into account when using modprobe. In addition, modprobe reads in the file `/etc/modprobe.conf` for any configuration settings.

  This command can only be used if the file `/lib/modules/version/modules.dep` created by the command depmod exists. This file is used to add or remove dependencies.

  The kernel daemon (Kmod since kernel version 2.2.x) ensures that modules needed in the running operation are automatically loaded using modprobe (such as accessing the CD-ROM drive).

  For more detailed information, enter man modprobe.

- **depmod.** This command creates the file `/lib/modules/version/modules.dep`. This file contains the dependencies of individual modules on each other.

  When a module is loaded (such as with modprobe), modules.dep ensures that all modules it depends on are also loaded.

  If the file modules.dep does not exist, it is created automatically when the system starts by the start script `/etc/init.d/boot`. For this reason, you do not need to create the file manually.

  On SUSE Linux Enterprise Server 10, depmod also creates the file modules.aliases, which is used by hwup and modprobe to determine which driver needs to be loaded for which device. Learn more about this file in the hwup objective in this section.

- **modinfo option module.** This command displays information (such as license, author, and description) about the module indicated on the command line.

  The following is an example:

  ```
DAS0:~ # modinfo isdn
license:        GPL
author:         Fritz Elfert
description:    ISDN4Linux: link layer
depends:        slhc
supported:      yes
vermagic:       2.6.5-7.21-default 586 REGPARM gcc-3.3
  ```

  For more detailed information, enter **man modinfo**.

## modprobe Configuration File (/etc/modprobe.conf)

The file /etc/modprobe.conf is the configuration file for the kernel modules. For example, it contains parameters for the modules that access hardware directly.

The file plays an important role in loading modules. Various command types can be found in the file, such as the following:

- **install.** These instructions let modprobe execute commands when loading a specific module into the kernel.

  The following is an example:

  `install eth0 /bin/true`

- **alias.** These instructions determine which kernel module will be loaded for a specific device file.

  The following is an example:

  `alias eth0 nvnet`

- **options.** These instructions are options for loading a module.

  The following is an example:

  `options ne io=0x300 irq=5`

For more detailed information, enter man 5 modprobe.conf.

![](img/8279afe915b153902294b0e58311b75a_56_0.png)
