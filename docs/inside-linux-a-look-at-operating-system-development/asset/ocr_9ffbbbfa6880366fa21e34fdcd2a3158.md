system servers and multi-user timeshare systems.

In some cases the system hardware has not advanced as quickly as the central processor. For instance, the IBM personal computer was designed for less than 1 Mbyte of memory at a time when no individual was likely to buy that much memory. This led to a decision to use locations above 640 Kbytes to address peripheral devices. Following this decision by IBM, Microsoft Corporation released an operating system which relied on an addressing mode which was normally limited to a 1 Mbyte address range.

Now that personal computer systems are commonly sold with 8 Mbytes of memory, the earlier decision looks foolish.

Fortunately this decision can be overcome through the appropriate use of memory mapping. In the case of MS-DOS, this memory mapping is still unwieldy because of a desire to maintain compatibility with old systems. Linux suffers less because it requires one of the later model Intel computers and it uses a convenient memory addressing scheme.

In a similar vein, the bus used to access peripherals was initially quite narrow (8 bits) and slow (5-10 MHz). Since then, improved buses have been designed to provide paths which are wider (32-64 bits) and faster (33 MHz).

# 8.1 Selection and Performance

The personal computer market has spawned an amazing number of different peripherals, some of which barely satisfy the bus standards and a few which don't quite meet the bus standards.

Because of its preeminent market position, MS-DOS does not have to directly support all these different peripherals. Peripheral manufacturers provide drivers for their devices in a ROM on the control card. The Basic Input/Output System incorporates these drivers as part of its interface to MS-DOS and to stand-alone programs. (We saw in Section 5.7.3 how these drivers are used by the Linux Loader (LILO).)

Although newer peripherals have correspondingly newer ROMs, the basic BIOS interface remains somewhat limited. For instance, it cannot directly address disk tracks beyond 1023 and it does not support multi-tasking use of peripherals because the subroutines are not re-entrant.