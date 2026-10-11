After the installation is complete you may want to rebuild a kernel that includes support for your specific hardware configuration. See Section 2.8, *Building a Custom Kernel* for information on building a customized kernel. Note that, in most cases, a custom-built kernel is not necessary.

# A.2 CD-ROM Module Parameters

> **Please Note**
> 
> Not all of the cards that are listed are supported. Please check the hardware compatibility list on Red Hat's World Wide Web site at http://www.redhat.com/support/docs/hardware.html to make sure your card is supported.

One of the more commonly used parameters, the `hdx=cdrom` parameter, `can` be entered at the boot prompt, as it deals with support for IDE/ATAPI CD-ROMs, which is part of the kernel.

In the tables below, most modules without any parameters listed are either able to auto-probe to find the hardware, or require you to manually change settings in the module source code, and recompile.

Table A–1 Hardware Parameters

| Hardware | Module | Parameters |
| :--- | :--- | :--- |
| ATAPI/IDE CD-ROM Drives | | hdx=cdrom |
| Aztech CD268-01A, Orchid CD-3110, Okano/Wearnes CDD110, Conrad TxC, CyCDROM CR520, CyCDROM CR540 (non-IDE) | aztcdo | aztcd=io_port |