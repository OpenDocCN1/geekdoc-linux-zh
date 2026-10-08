# THE WINDOWS EMULATOR Wine 369

This kind of control is a visible break in the use of the X Window system, but no better solution is currently in sight. One possibility would be the development of a Windows-compatible window manager. On my own system, I use fwm95, which emulates the interface of Windows 95 together with the -desktop option.

# 12.2.4 Additional features

The development of Wine is not aimed at creating a Windows emulator for LINUX and *BSD systems, but other operating systems too, which do not run on Intel processors. For this purpose, Bochs, a (shareware) CPU emulator for Intel CPUs, could be used.
A further function of Wine is the use as a library for porting Windows programs to arbitrary UNIX/X systems. This library has already been employed to implement a program manager and a helper browser. Both programs are included in the Wine sources, but are not automatically installed.

For debugging purposes, Wine contains its own debugger which can work in both 16-bit and 32-bit mode. Initially, the GNU debugger was used, but because of the GL restrictions, it was replaced with the Mach debugger.

# 12.2.5 Further development

Many features are still to be implemented to complete the emulator. Important functions that are currently still lacking are the representation of different fonts, in particular TrueType fonts, a device-independent printer control, and functions such as DDE and ODE. Besides, the implementation of the Win32 interface is being worked upon to allow processing of Windows 95 programs.

In addition, a manual is under development which is currently supplied in Texinfo format. It describes the emulator and documents the implemented API.

| Additional Information and Sources |
| --- | --- |
| Newsgroup: | comp.emulator.ms-windows.wine |
| ftp server: | tsx-11.mit.edu |
| ftp path: | /pub/linux/ALPHA/Wine/development |
| Package: | Wine-date.tar.gz |
| Size: | about 1.6 Mbytes |
| Homepage: | http://www.winehq.com |