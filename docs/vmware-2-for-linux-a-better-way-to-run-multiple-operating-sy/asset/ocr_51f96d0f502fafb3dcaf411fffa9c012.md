VMware should work with any Linux networking card. Instead of giving guest operating systems direct access to your network adapter, however, VMware internally emulates an AMD PCnet Family Ethernet card, so that is the device each guest operating system must be able to support. Every VMware certified guest OS supports the PCnet Family emulation, including DOS and Windows 3.1.

> Full documentation and device drivers for the PCnet Family card are available at http://www.amd.com/products/npd/software/pcnet_family/intro.html.

# SCSI

The only SCSI hardware VMware can access are hard drives and CD-ROMs. Scanners, tape drives, and other peripherals are unavailable.

VMware’s SCSI support is similar to its Ethernet card support. Instead of allowing the virtual machine to see your SCSI card directly, VMware emulates its own SCSI card, in this case a BusLogic BT-958 device. This card is supported in all of VMware’s supported guest operating systems.

The emulated SCSI card can see up to seven devices (virtual disks and CD-ROM devices combined), in addition to what the emulated IDE controller can support.

> For more information on the BusLogic BT-958, see the manufacturer’s support page at http://www.mylex.com/support/download/manuals/scsihstad.html.

# Sound Cards

Sound support under Linux is certainly a lot better than it has been in years past, but it’s still not an exact science, in large part because sound card manufacturers keep changing their chips and specifications without telling anybody.

Some card families, such as those from Creative Labs and ESS, are reasonably well supported by Linux developers. Some vendors, such as Aureal, have begun supporting Linux directly—although Aureal is now bankrupt.

If you’ve managed to conquer the challenges of sound configuration in Linux, VMware will richly reward you with SoundBlaster 16 emulation in its virtual machines. VMware does not currently support MIDI synthesis or the joystick port found on most audio cards.