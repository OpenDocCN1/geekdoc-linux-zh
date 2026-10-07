# MORE READING

This chapter covered methods available on Linux to debug a USB system. These methods will serve the debugging needs of any USB developer. Linux documentation available at /Documentation/usb/usbmon.txt includes additional information about usbmon.

The usbmon developer's white paper is available at http://people.redhat.com/zaitsev/linux/OLS05_zaitcev.pdf. There you'll find more insights into the design and architecture.

As referred to in this chapter, usbmon implements a more comprehensive binary reader that provides access to complete URB information. To learn more about the binary version of usbmon, explore drivers /usb/mon /mon_bin.c.

A more detailed article titled “Snooping the USB Data Stream” is available on the Linux journal at http://www.linuxjournal.com/article/7582.