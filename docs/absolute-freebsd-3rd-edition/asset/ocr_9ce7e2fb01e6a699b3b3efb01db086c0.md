A common place to keep a known good kernel is /boot/kernel.good. Back up your working, reliable kernel like this:

```
# cp -a /boot/kernel /boot/kernel.good
```

If you’re using ZFS, a boot environment might make more sense than copying (see Chapter 12).

Don’t be afraid to keep a variety of kernels on hand. Disk space is cheaper than time. I know people who keep kernels in directories named by date so that they can fall back to earlier versions if necessary. Many people also keep a current copy of the GENERIC kernel in /boot/kernel.GENERIC for testing and debugging purposes. The only way to have too many kernels is to fill up your hard drive.

# Configuration File Format

FreeBSD’s kernel is configured via text files. There’s no graphical utility or menu-driven system for kernel configuration; it’s still much the same as in 4.4 BSD. If you’re not comfortable with text configuration files, building a kernel is just not for you.

Each kernel configuration entry is on a single line. You’ll see a label to indicate what sort of entry this is, and then a term for the entry. Many entries also have comments set off with a hash mark, much like this entry for the FreeBSD filesystem FFS:

```
options		FFS		# Berkeley Fast Filesystem
```

Every complete kernel configuration file is made up of five types of entries: cpu, ident, makeoptions, options, and devices. The presence or absence of these entries dictates how the kernel supports the associated feature or hardware:

+   - cpu This label indicates what kind of processor this kernel supports.

The kernel configuration file for the boring old PC hardware includes several CPU entries to cover processors such as the 486 (I486_CPU), Pentium (I586_CPU), and Pentium Pro through modern Pentium 4 CPUs (I686_CPU). The kernel configuration for