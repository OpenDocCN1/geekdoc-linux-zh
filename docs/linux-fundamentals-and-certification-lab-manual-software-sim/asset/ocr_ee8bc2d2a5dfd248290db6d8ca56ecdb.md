In this case the version is 0.93 and the build number is 4. If GRUB is not installed, it may be located on the Linux distribution disk or it can be downloaded from several Internet locations.

From the command prompt you can execute the command `grub-install <location>` where `<location>` is the location where grub should be installed. If grub needs to be installed on the MBR of the first hard drive, you would type the `grub-install /dev/hda` command:

# NOTE

The location of the grub-install program can be found with the rpm query program (`rpm -ql grub`).

If another boot loader is already installed, it does not have to be removed before installing GRUB. After GRUB is installed, reboot the computer to see the new GRUB boot loader.

# Booting an Operating System with GRUB

GRUB has two boot methods—load an operating system directly and chain-load another boot loader, which will then boot the operating system. Typically, GRUB will load an operating system directly, but GRUB doesn't support all operating systems, so the chain-load method is necessary.

GRUB is designed to boot multiboot-compliant kernels. Other operating systems require OS-specific commands.

GRUB stores information in a configuration file. GRUB has three interfaces that provide different levels of functionality. Each interface provides commands to boot operating systems.

The **menu** interface provides a menu of operating systems preconfigured with their own boot commands. The arrow keys can be used to select the operating system (OS) to boot. The default OS will boot after a preset timeout period.

The **menu entry editor** interface is displayed by pressing the character **e** while the menu interface is displayed. The menu entry editor allows command lines to be changed before booting the operating system.

The **command-line** interface is very basic, but it allows the most control of the boot process. Within the command line interface, any valid GRUB command can be executed.

When GRUB starts, it looks for its configuration file. When this file is found GRUB uses it to build the menu list of operating systems, then displays the menu interface. If the configuration file is not present, GRUB will load the command line interface to allow entering commands directly to start the operating system.

# GRUB Commands

GRUB provides several commands that can be used in its interfaces to start operating systems. A full list of commands is displayed by typing the `info grub` command. Some of the commands are:

+   - **boot**: Boots the operating system or chain loader specified. This command is entered after boot parameters are defined.
- **chainloader <filename>**: Loads the specified file as a chain loader. A + 1 can be entered to use the file at the first sector of the specified partition.
- **initrd <filename>**: Specify an initial RAM disk to use when booting.
- **kernel <kernel_filename> options**: Specifies the kernel file to load.
- **root <device_partition>**: Configures the root partition to be used and mounts the partition.