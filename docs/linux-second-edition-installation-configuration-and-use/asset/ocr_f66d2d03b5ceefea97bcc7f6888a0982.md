# Booting from hard disk

If start-up (without a boot diskette, straight from the hard disk) LILO: is displayed and nothing happens, things are probably OK: LILO waits for you to specify which operating system the computer should be booted. First, press Shift, then Tab, LILO displays the operating systems that can be selected. Use the keyboard to enter a name and press

Things are worse if LILO does not react to any input, displays lots of zeros and so on. In this case, something has probably gone wrong with the LILO installation. If you work with DOS or Windows, the simplest solution is to restart the computer with a DOS boot diskette and execute FDISK /MBR. This overwrites the boot sector and at next restart, DOS/Windows should come up normally. Until your next LILO installation, you can start Linux with no boot diskette.

If apart from Linux, you have not installed DOS/Windows, but a different operating system (OS/2, Windows NT, and so on), reconstitution of the boot sector is a bit more difficult. You must start Linux with a boot diskette and reinstall the original boot sector saved during LILO installation. You can read more about this and about a correct (and safe) installation of LILO on page 183.

# Memory problems (RAM)

Linux is partly programmed very close to the hardware. It optimally exploits your hardware and in many respects offers better performance than other operating systems. This closeness to the hardware can, however, cause Linux (as opposed, for example, to Windows) to become unstable.

The reason is in most cases an incorrect BIOS configuration of the computer. In the BIOS, you can specify the number of wait states used to access the RAM. In general, the more waits, the slower. Therefore, the number of wait states is often set to a very low value by users or producers. Depending on the access time and the quality of your RAM chips, the computer may keep running under Windows, but may fail under Linux.

There are two Linux tools which allow you to perform a memory test. memtest86 is a mini kernel whose only task is an endless memory test. (You need to boot your computer with this system from a diskette. Then you can run the test over night.) The memtest command, in contrast, can be used to test memory during normal operation.