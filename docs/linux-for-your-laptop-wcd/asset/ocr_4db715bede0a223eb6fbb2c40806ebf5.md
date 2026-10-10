Be careful that settings in your XF86Config do not stress or attempt to push the external monitor beyond its capabilities. Be sure to read the technical details about your notebook's external video port first!

# Infrared Port

Many notebooks come equipped with an IrDA port for wireless communication, such as networking, file transfers, and printing. The IrDA port may be located on either side or the back of your laptop. In order to use the port, you must enable IrDA on your notebook and then place the remote device within range of the port, most likely within 3 meters and possibly within a range as shallow as 15 degrees.

For initial pointers about using IrDA with Linux, look for a short text file named irda.txt under the /usr/src/linux/Documentation/networking directory (make sure you have installed the kernel sources). However, with the rapid development of the Linux kernel, documentation and guidelines for setting up and performing IR for networking, file transfer, and printing with Linux are pretty sparse; IrDA development under Linux is a moving target. A good place to start is

http://www.cs.uoit.no/linux-irda/

You'll find several links and information. You can also check for compatibility with your notebook at

http://www.cs.uoit.no/linux-irda/hardware.html

If you want to learn more about IrDA and get some practical applications for Linux, some documentation is contained in the Linux IR-HOWTO by Werner Heuser, available at

http://www.enfu.de/~wehe/IR-HOWTO.html

# Installing IrDA Support

The first step is to install IR services. IrDA support for Linux is now part of the 2.2.X series of Linux kernels, but you must download and install Dag Bratl's package of software named irda-utils. Then you must build and install the support libraries and at least two utilities: irdattach and irdamanger. You can find this software at

http://www.cs.uoit.no/linux-irda/irda-utils/

After the building and installing, several commands and files are copied into your filesystem. You then need to enable IR and determine the port size. Some notebooks provide a special Fn key combination to turn on IR, while on others you