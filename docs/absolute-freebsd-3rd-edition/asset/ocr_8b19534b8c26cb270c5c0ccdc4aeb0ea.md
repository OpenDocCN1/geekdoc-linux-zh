If you get this far and still have a problem, you might actually need to file a bug report. Let’s see what not to put in it.

# Bad Bug Reports

The easiest way to understand a good bug report is to read some bad ones and identify what makes them bad. Digging through the closed bugs uncovers bunches of bad reports, but here’s an archetype:

> When I boot the FreeBSD 12.1 ISO image, I can’t get past the “Welcome to FreeBSD” options screen. The boot menu is stuck, and each time the screen refreshes it stays at 10. It doesn’t matter what I press, the system never boots. If I press a whole bunch of buttons, I eventually get a kernel panic. The same ISO image launches in VirtualBox and I can install it to the disk.

The bug report includes the model number of a dead standard SuperMicro motherboard, keyboard, and mouse. None of the hardware is exotic. The reporter suggests reproducing the problem by booting the ISO with similar hardware.

First off, the reporter obviously has a problem installing FreeBSD. It might even be that FreeBSD has a problem. I’ve no doubt that this system fails at boot exactly as advertised. But there’s no evidence and no diagnostic information. The reproduction process isn’t very useful; if every 12.1 installation image behaved this way on common hardware, the release engineers would have never signed off on the release.

Including the hardware make and model isn’t as useful as you might hope. Vendors occasionally change chipsets without changing the model number. The verbose boot information identifies the hardware in the machine in a way that the model number never can. This reporter can’t get a 12.1 verbose boot, however.

If I experienced this behavior, I’d first try a second CD. Perhaps the first burned disk was bad. If the behavior persisted, I’d download a slightly older version of FreeBSD to see whether the problem exists there. If 12.0 fails, how about 11.0? I’d include the verbose boot