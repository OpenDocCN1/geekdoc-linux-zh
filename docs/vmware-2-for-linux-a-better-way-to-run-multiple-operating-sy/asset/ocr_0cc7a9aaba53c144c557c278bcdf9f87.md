the NT4/2000 version.) Users of Win 95 or Win 98 do not have to do anything special.

+   5. If you want the Mac emulation to have access to your CD-ROM drive (and you should), you need to copy a driver to your CD-ROM drive (and you should), you need to copy a driver to the Windows system directory. 95/98 users will find their driver, cdenable.vxd, in the CD-ROM drivers/9x directory and should copy that file to C:\Windows\System. For NT 4/2000 VMs, copy the file cdenable.sys in CD-ROM drivers/NT4 and Win2k to C:\WinNT\System32\drivers.

+   6. Copy the Macintosh ROM file (see the section "Making Sense of Legalities" earlier in this chapter for details) into the same directory with the main BasiliskII.exe file. Name it something sensible, such as ROM or basilisk.rom.

# Configuring Basilisk II

Although the Linux and Windows versions of Basilisk II are just about functionally equivalent, their configuration interfaces are quite a bit different. The Windows version has a thorough (but somewhat imposing) GUI configuration program, and the Linux version has a GUI configuration window that is much easier to use but offers fewer features.

> Basilisk II is technically capable of sharing an Ethernet connection with your PC. But the sharing driver does not seem to work properly in VMware, and the Linux version requires the use of the Basilisk II source code or the Linux etherapt system, both of which are advanced configuration options best left alone unless you are absolutely sure you need them. Consult the Basilisk II documentation for details.

![](bbox=[0.07, 0.75, 0.18, 0.88])

# Configuring Basilisk II for Linux

Mercifully, recent versions of Basilisk II have added a GUI configuration interface as a front-end to its text-based configuration file.

+   1. Type BasiliskII at a command prompt to launch the emulator. The GUI configuration window should appear, as shown in Figure 17.9.

+   2. You should start with the first tab, Volumes. You need to create a hardfile (similar to a VMware virtual disk, except it immediately takes up all the requested space). Click the Create button, and create a hardfile in your Basilisk II files directory. Use a simple name, such as macdisk.HFV. (HFV is a common extension for Mac hardfiles.) The size of the disk is up to you, but I recommend at least 100MB.