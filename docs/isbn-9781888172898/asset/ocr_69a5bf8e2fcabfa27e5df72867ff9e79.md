# D.5.  **HOW TO LOAD MILO**

0x100000. For this reason, MILO is built with its PALcode starting at 0x200000. When it is first loaded, it moves itself to the correct location (see relocate.S).

# AlphaPC64 (CabrioleT)

The AlphaPC64 includes the Windows NT ARC firmware (Section D.5.1), the SRM Console (Section D.5.6) and the Evaluation Debug Monitor (Section D.5.3). These images are in flash and there is room to add MILO so that you can boot MILO directly from flash. A flash management utility, runnable from MILO is available so that once MILO is running, it can be blown into flash (Section D.7). This system supports MILO environment variables.

You select between the boot options (and MILO when it is been put into flash) using a combination of jumpers and a boot option which is saved in the NVRAM of the TOY clock.

The jumper is J2, SP bits 6 and 7 have the following meanings:

+   - SP bit 6 should always be out. If this jumper is set then the SROM mini-debugger gets booted.
+   - SP bit 7 in is boot image selected by the boot option byte in the TOY clock.
+   - SP bit 7 out is boot first image in flash.

So, with bit 7 out, the Debug Monitor will be booted as it is always the first image in flash. With bit 7 in, the image selected by the boot option in the TOY clock will be selected. The Debug Monitor, the Windows NT ARC firmware and MILO all support setting this boot option byte but you must be very careful using it. In particular, you cannot set the boot option so that next time the system boots MILO when you are running the Windows NT ARC firmware, it only allows you to set Debug Monitor or Windows NT ARC as boot options.

To get MILO into flash via the Evaluation Board Debug Monitor, you will need a flashable image. The build procedures make MILO.rom, but you can also make a rom image using the makerom tool in the Debug Monitor software that comes with the board: