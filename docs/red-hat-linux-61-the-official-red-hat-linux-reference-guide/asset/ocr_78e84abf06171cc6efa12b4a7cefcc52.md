# Appendix A. General Parameters and Modules

# A.2. CD-ROM Module Parameters

Note

Not all of the CD-ROM drives that are listed are supported. Please check the Hardware Compatibility List on Red Hat's website at http://hardware.redhat.com to make sure the device is supported.

Even though parameters are specified after loading the driver disk and specifying the device, one of the most commonly used parameters hdx=cdrom (where X corresponds to the appropriate drive letter) can be entered at a boot prompt during installation. This is allowed since it IDE/ATAPI CD-ROMs, which are already part of the kernel.

In the following tables, most modules listed without any parameters either be auto-probed to the hardware or require manual changes to settings in the module source code and a recompile.

| Hardware | Module | Parameters |
| --- | --- | --- |
| ATAPSI/IDE CD-ROM Drives | | hdx=cdrom |
| Aztech CD268-01A, Orchid CD-3110, Okano/Wearneas CDD110, Conrad TXC, CyCDROM CR520, CyCDROM CR540 (non-IDE) | aztcd.o | aztcd=io_port |
| Sony CDU-31A CD-ROM | cdu31a.o | cdu31a=io_port,IRQ OR cdu31a_port=base_addr cdu31a_irq=irq |
| Philips/LMS CD-ROM driver 206 with cm260 host adapter card | cm206.o | cm206=io_port,IRQ |
| Goldstar R420 CD-ROM | gscd.o | gscd=io_port |
| ISP16, MAD16, or Mozart sound card CD-ROM interface (OptI 82C28 and OptI 82C29) with Sanyo/Pansonic, Sony, or Mitsumi drives | isp16.o | isp16=io_port,IRQ,dma,drive_type=OR isp16_cdrom_base=io_port isp16_cdrom_irq=irq isp16_cdrom_dma=dma isp16_cdrom_type=drive_type |
| Mitsumi CD-ROM, Standard | mcd.o | mcd=io_port,IRQ |
| Mitsumi CD-ROM, Experimental | mcdx.o | mcdx=io_port_1,IRQ_1,io_port_n,IRQ_n |
| Optics storage "Dolphin" drive, Lasermate CR328A | optcd.o | |
| Parallel-Port IDE CD-ROM | pcd.o | |
| SB Pro 16 Compatible | sbpcd.o | sbpcd=io_port |
| Sanyo CDR-H94A | sjcd.o | sjcd=io_port OR sjcd_base=io_port |