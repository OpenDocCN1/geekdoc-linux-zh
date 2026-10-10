# 5.7. BOOTSTRAPPING THE KERNEL

LILO is a suite of programs including the installation utility `/sbin/lilo` and the primary and secondary bootstrap programs `/boot/boot.b`. `/sbin/lilo` extracts the primary bootstrap program code from `/boot/boot.b` and writes it, along with data describing important disk addresses, onto the disk's boot sectors. The primary and secondary bootstrap programs perform the actual loading of the system.

![](bbox=[0.1, 0.27, 0.95, 0.57])

The BIOS loads the 512 bytes of primary bootstrap to location 0x7C00. The primary bootstrap relocates itself to 0x9A000 and it then calls upon the BIOS to load up to 8 kbytes of the secondary bootstrap starting at 0x9B000.

(By using the drivers within the BIOS, the primary and secondary bootstraps avoid the need to containing any device dependent code at all. This elegant technique is marred by an unfortunate problem: the parameters passed for a BIOS disk read are not sufficient to reference high numbered cylinders. Therefore, LILO cannot load sectors which are located in disk cylinders above 1023.)

The secondary bootstrap presents messages from `/boot/message` and reads options and image names from `/boot/map`. After some optional interaction with the user, it loads a kernel image from the locations given in the pointer part of `/boot/map`.