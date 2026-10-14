board address and interrupt assignments. The cards also contain descriptions of the resources which need to be allocated. The BIOS on your system, or isapnp tools, uses a protocol described in the specification to find all of the PnP boards and allocate the resources so that none of them conflict. Note that the BIOS doesn't do a very good job of allocating resources. So isapnptools is suitable for all systems, whether or not they include a PnP BIOS. In fact, a PnP BIOS adds some complications. A PnP BIOS may already activate some cards so that the drivers can find them. Then these tools can unconfigure them or change their settings, causing all sorts of nasty effects. If you have PnP network cards that already work, you should read through the documentation files very carefully before you use isapnptools. Install isapnptools if you need utilities for configuring ISA PnP cards.

# kbdconfig -- (Version 1.9, 40K)

[B]

The kbdconfig utility is a terminal mode program for setting the keyboard map for your system. Keyboard maps are necessary for using any keyboard besides the US default keyboard. Kbdconfig will load the selected keymap before exiting and configure your machine to use that keymap automatically after rebooting. You should install kbdconfig if you need a utility for changing your keyboard map.

# ld.so -- (Version 1.9.5, 247K)

[B]

This package contains the shared library configuration tool, ldconfig, which is required by many packages. It also includes the shared library loader and dynamic loader for Linux libc 5.

# ldconfig -- (Version 1.9.5, 223K)

[B]

Ldconfig is a basic system program which determines run-time link bindings between ld.so and shared libraries. Ldconfig scans a running system and sets up the symbolic links that are used to load shared libraries properly. It also creates a cache (/etc/ld.so.cache) which speeds the loading of programs which use shared libraries.

# lilo -- (Version 0.21, 1,095K)

[B]

LILO (Linux LOader) is a basic system program which boots your Linux system. LILO loads the Linux kernel from a floppy or a hard drive, boots the kernel and passes control of the system to the kernel. LILO can also boot other operating systems.