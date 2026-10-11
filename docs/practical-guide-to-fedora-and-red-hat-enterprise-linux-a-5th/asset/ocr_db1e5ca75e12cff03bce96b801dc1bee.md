Presentsa a choice of installation sources: local CD/DVD or hard disk, or over a network using NFS, FTP, or HTTP (first installation CD, Net Boot CD, and install DVD only).

+   • **Local CD/DVD**—Displays the Disc Found screen, which allows you to test the installation media (the same as if you had not entered any boot parameters).

+   • **Hard drive**—Prompts for the partition and directory that contain the installation tree or the ISO image of the install DVD. Do not include the name of the mount point when you specify the name of the directory. For example, if the ISO images are in the /home/**sam**/FC12 directory and /dev/sda6 holds the partition that is normally mounted on /home, you would specify the partition as /dev/sda6 and the directory as **sam**/FC12 (no leading slash).

+   • The next two selections display the Configure TCP/IP screen from which you can select DHCP or Manual configuration. Manual configuration requires you to enter the system’s IP address and netmask as well as the IP addresses of the default gateway and primary nameserver.

+   ♦ **NFS directory**—Displays the NFS Setup screen, which requires you to enter the NFS server name and the name of the directory that contains the installation tree or the ISO image of the install DVD. Enter the server’s IP address and the *name* of the exported directory, not its device name. The remote (server) system must export (page 739) the directory hierarchy that holds the installation tree or the ISO image of the install DVD.

+   ♦ **URL**—Displays the URL Setup screen, which requires you to enter the URL of the directory that contains the installation tree or the ISO image of the install DVD.

**nodma**   Turns off direct memory access (DMA) for all disk controllers. This parameter may make buggy controllers (or controllers with buggy drivers) more reliable, but also causes them to perform very slowly because the connected devices have to run in PIO mode instead of DMA mode. It may facilitate testing CD/DVDs that were not written correctly. For more information refer to “The Disc Found Screen” on page 57.

**nofb**   (no **framebuffer**) Turns off the framebuffer (video memory). This option is useful if problems arise when the graphical phase of the installation starts.

**irqpoll**   Changes the way the kernel handles interrupts.

**ks=URI**   Specifies the location of a Kickstart (page 82) file to use to control the installation process. The *URI* is the pathname or network location of the Kickstart file.

**noapic**   Disables local APIC. The default is to enable local APIC.

**lowres**   Runs the installation program at a resolution of 640 × 480 pixels. See also **resolution**.