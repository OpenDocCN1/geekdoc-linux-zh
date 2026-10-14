
## urw-fonts -- (Version 1.1, 2,160K)

Free versions of the 35 standard PostScript fonts. With newer releases of ghostscript quality versions of the standard 35 Type 1 PostScript fonts are shipped. They were donated and licensed under the GPL by URW. The fonts.dir was specially made to match the original Adobe names of the fonts, e.g. Times, Helvetica etc. With X, LaTeX, or Ghostscript, these fonts are a must to have!

## x3270 -- (Version 3.1.1.6, 561K)

The x3270 program opens a window in the X Window System which emulates the actual look of an IBM 3278/3279 terminal, commonly used with mainframe applications. x3270 also allows you to telnet to an IBM host from the x3270 window. Install the x3270 package if you need to access IBM hosts using an IBM 3278/3279 terminal emulator.

## xinitrc -- (Version 2.1, 8K)

The xinitrc package contains the xinitrc file, a script which is used to configure your X Window System session or to start a window manager. The xinitrc package should be installed if you use the X Window System.

## Appendix D: General Parameters and Modules

This appendix is provided to illustrate some of the possible parameters that may be needed by certain drivers. It should be noted that, in most cases, these additional parameters are unnecessary. Also included is a list of network hardware and the associated modules required by that hardware. Please keep in mind that if a device you are attempting to use requires one of these parameters, and support for that device is not compiled into the kernel, the traditional method of adding the parameter to the LILO boot command will not work. Drivers loaded as modules require that these parameters are specified when the module is loaded. The Red Hat Linux installation program gives you the option to specify module parameters when a driver is loaded. For more information concerning the device support compiled into the kernel used by the Red Hat Linux installation program, please refer to Section 2.9.

Please Note: Not all of the cards that are listed are supported. Please check the hardware compatibility list on Red Hat Software's World Wide Web site at http://www.redhat.com/support/docs/hardware.html to make sure your card is supported.

One of the more commonly used parameters, the `hdX=cdrom` parameter, can be entered at the boot prompt, as it deals with support for IDE/ATAPI CD-ROMs, which is part of the kernel.

In the tables below, most modules without any parameters listed are either able to auto-probe to find the hardware, or require you to manually change settings in the module source code, and recompile.

### CD-ROM parameters

| Hardware | Module | Parameters |
|---|---|---|
| ATAPI/IDE CD-ROM Drives |  | hdX=cdrom |
| Aztech CD268-01A, Orchid CD-3110, Okano/Weames CDD110, Conrad TXC, CyCDROM CR520, CyCDROM CR540 (non-IDE) | aztcd.o | aztcd=io_port |
| Sony CDU 31A or 33A CD-ROM | cdu31a.o | cdu31a=io_port,IRQ,PAS<br>cdu31a_port=base_addr<br>cdu31a_irq=irq |
| Philips/LMS CDROM drive 206 with cm260 host adapter card | cm206.o | cm206=io_port,IRQ |
| Goldstar R420 CD-ROM | gscd.o | gscd=io_port |
| ISP 16, MAD16, or Mozart sound card CD-ROM interface (OPTi 82C928 and OPTi 82C929) with Sanyo/Panasonic, Sony, or Mitsumi drives | isp16.o | isp16=io_port,IRQ,dma,drive_type<br>isp16_cdrom_base=io_port<br>isp16_cdrom_irq=IRQ<br>isp16_cdrom_dma=dma<br>isp16_cdrom_type=drive_type |
| Mitsumi CD-ROM, Standard | mcd.o | mcd=io_port,IRQ |
| Mitsumi CD-ROM, Experimental | mcdx.o | mcdx=io_port_1,IRQ_1,io_port_n,IRQ_n |
| Optics storage 8000 AT CD-ROM; "Dolphin" drive; Lasermate CR328A | optcd.o | optcd=io_port |
| SB Pro 16 compatible | sbpcd.o | sbpcd=io_port,sb_pro_Setting |
| Sanyo CDR-H94A | sjcd.o | sjcd=io_port,sjcd_base=io_port |
| Sony CDU-535 & 531 (some Procomm drives) | sonycd535.o | sonycd535=io_port |
