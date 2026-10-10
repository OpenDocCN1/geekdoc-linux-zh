you have more than one floppy drive. Floppy disks aren't partitioned, so they don't receive partition numbers.

GRUB defines its own root partition, which can be different from the Linux root parti-tion. GRUB's root partition is the partition in which GRUB's configuration file (*menu.lst* or *grub.conf*) resides. Because this file is normally in Linux's */boot/grub/* directory, the GRUB root partition will be the same as Linux's root partition *if you do not use a separate /boot or /boot/grub partition.* If you split off */boot* into its own partition, as is fairly com-mon, GRUB's root partition will be the same as Linux's */boot* partition. You must keep this difference in mind when referring to files in the GRUB configuration directory.

# Essential Global GRUB Options

GRUB's global section precedes its per-image configurations. Typically, you'll find fewer options in this global section than in a LILO global configuration:

**Default OS** The *default=* option tells GRUB which OS to boot. Listing 5.2's *default*=0 causes the first listed OS to be booted (remember, GRUB indexes from 0). If you want to boot the second listed operating system, use *default*=1, and so on through all your OSs.

**Timeout** The *timeout=* option defines how long, in seconds, to wait for user input before booting the default operating system. Note that GRUB measures its timeout period in seconds, whereas LILO uses tenths of a second.

**Background graphic** The *splashimage=* line points to a graphics file that's displayed as the background for the boot process. This line is optional, but most Linux distributions point to an image to spruce up the boot menu. The filename reference is relative to the GRUB root partition, so if */boot* is on a separate partition, that portion of the path is omitted. Alterna-tively, the path may begin with a GRUB device specification, such as (*hd0*,5) to refer to a file on that partition.

# Essential GRUB Per-Image Options

GRUB's per-image options are typically indented after the first line, much like LILO's, but this is a convention, not a requirement of the file format. The options begin with an identi-fication and continue with options that tell GRUB how to handle the image:

**Title** The *title* line begins a per-image stanza and specifies the label to display when the boot loader runs. Unlike LILO's *label* option, the GRUB *title* can accept spaces and is conventionally much more descriptive, as shown in Listing 5.2.

**GRUB root** The *root* option specifies the location of GRUB's root partition. This is the */boot* partition if a separate one exists; otherwise it's usually the Linux root */* partition. GRUB *can* reside on a FAT partition, on a floppy disk, or on certain other OSes' parti-tions, though, so GRUB's root could conceivably be somewhere more exotic.

**Kernel specification** The *kernel* setting describes the location of the Linux kernel as well as any kernel options that are to be passed to it. Paths are relative to GRUB's root partition. As an alternative, you can specify devices using GRUB's syntax, such as *kernel* (*hd0*,5) */vmlinuz ro root=/dev/hda5.* Note that you pass most kernel options on this line. LILO splits off kernel options on separate lines, such as the *append=* line, the *root=* line, and