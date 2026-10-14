# Figure 14-2: Linux Bootup Configuration

Clicking one of the boot kernel or boot partition icons will allow you to edit that boot kernel or partition (Figure 14-3).

# Figure 14-3: Edit Boot Kernel

Here the name is an identifier for the kernel and it translates to label in the /etc/lilo.conf file. The Kernel to boot is the path to the Linux kernel boot image to load.

# Kernel options

This field can be used to enter any arguments you need to pass to your kernel on boot. It is often used for specifying the amount of memory in a machine when Linux doesn’t recognize it all. For example, to specify 127MB of RAM, one could select Add options and add the line mem=127M in the text field. This will be translated in the /etc/lilo.conf file to: