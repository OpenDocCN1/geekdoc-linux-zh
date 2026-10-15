The Apple Macintosh operating system is actually distributed in two pieces. There is the conventional OS CD that you install and run on a Mac or an emulator, but there is another invisible portion: the Macintosh ROM, a chip or pair of chips inside the computer that contain low-level code to boot the rest of the MacOS. Although you do not need to plug the chips into your computer to make Macintosh emulation work, you might need the code contained on those ROMs, depending on which emulator you choose to run.

The MacOS ROM is roughly akin to a PC’s BIOS, although it is more sophisticated and contains more code.

> VMware saves users the trouble of seeking out a ROM by licensing the Phoenix BIOS code for its virtual machines.

Executor’s MacOS simulation layer avoids any legal complication for the end user because you do not need either the MacOS CD or the ROM code to run Executor. Because ARDI does not use any of Apple’s proprietary code in the Browser and the emulation engine, Executor provides a no-hassle way to start running Macintosh software fast. The price of convenience is that Executor is a commercial product.

Although Basilisk II is an open-source program with no license fee, that doesn’t make its emulation system “free.” You need a copy of both the Mac’s ROM and the MacOS.

You can buy a MacOS CD from a store or even download an older version for free from Apple’s Web site. But it is a little more difficult to come by the ROMs. Without them, Basilisk II is useless.

The ROM code is copyrighted by Apple and cannot be freely distributed. It is still possible to observe the law and emulate the Mac, however. Following are the most popular ways to obtain legitimate copies of the ROM code:

+   - Strip the ROM code from a 68K Mac you already own. The Windows version of Basilisk II contains a tool for this (GetRom), as does the demo version of SoftMac 2000 (available from http://www.emulators.com). When you run Basilisk’s GetRom or SoftMac’s CopyROM on a 68K Macintosh (it should be a Mac II or newer), it creates a binary file containing the ROM code. That file can then be transferred to your PC and used for Mac emulation. Typically, you can use a standard MS-DOS formatted high-density floppy to transfer the ROM (which will be either 512KB or 1MB in length) from the Mac to your Linux PC.

+   - Obtain a set of ROMs from a Macintosh parts/repair vendor, and then use either a real Macintosh and the CopyROM program, or special ROM-reading equipment, to obtain the necessary binary file.