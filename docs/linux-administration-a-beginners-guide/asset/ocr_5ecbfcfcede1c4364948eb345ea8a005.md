# CODE MATURITY LEVEL OPTIONS

This menu has only one option: Do you want access to the latest and greatest (and therefore possibly experimental) kernel developments? Your answer to this question determines what items are available in the rest of the menu. Obviously, a production server should not be running experimental code. On the other hand, if you're planning to play with a system on your desk and are willing to take a few chances, that experimental code may offer some beneficial and interesting functions. (In general, even the experimental code is stable enough for day-to-day work. Rarely does a released feature cause a system to crash—but it does happen.)

# PROCESSOR TYPE AND FEATURES

This is another relatively self-explanatory list of setup items. The 2.2.10 kernel has only four questions:

+   - What kind of processor are you running?
+   - Do you need math emulation? (Necessary for running the kernel on 386, 386SX, or 486SX systems—yes, they're still out there!)
+   - Do you want to take advantage of memory registers?
+   - Do you want the kernel to have SMP chip support? (This lets you take advantage of systems with multiple CPUs.)

# LOADABLE MODULE SUPPORT

These questions determine whether you want support for modules, as described earlier in this section. Unless you have a specific need to avoid them, you should answer yes to this series of questions.

# GENERAL SETUP

This menu is critical in the grand scheme of kernel configuration. Your setup decisions here will enable and disable other items, so choose carefully.

All the options are self-explanatory except the item for binary file-type support. Not too long ago, compiled programs were stored in a file format known as a.out. Unfortunately, this scheme had severe limitations when it came to shared libraries, which became more of an issue as UNIX evolved. The ELF format was created to address these limitations and then done some. Linux currently uses the ELF binary format for all of its programs. Your system is unlikely to need a.out support, and you can safely say No to this option.

# PLUG AND PLAY SUPPORT

Sometimes this feature is more affectionately called “Plug and Pray Support.” Linux’s support for PnP devices does work; the nature of PC-based hardware, however, makes it unreliable. In general, defining what you need from the system is a safer course than relying on PnP to find it for you.

# BLOCK DEVICES

This menu lists the Linux support options for devices such as hard disks and CD-ROMs, including many options specific to chips. Unless you are certain of your particular chipset, you will want to leave these enhancement settings. Linux’s default behavior should work fine.

# NETWORKING OPTIONS

At a minimum, you should enable the UNIX Domain Sockets and TCP/IP Networking options.