# Examining your DASD

To obtain a list of all of the virtual DASD devices that are available to you, use the QUERY VIRTUAL DASD command; see Example 5-33.

Example 5-33 Output from the QUERY VIRTUAL DASD command

```
QUERY VIRTUAL DASD
DASD 0190 3390 LX6RES R/O 107 CYL ON DASD CD31 SUBCHANNEL = 0005
DASD 0191 3390 DKCD37 R/W 005 CYL ON DASD CD37 SUBCHANNEL = 0000
DASD 019D 3390 LX6W01 R/O 146 CYL ON DASD CD32 SUBCHANNEL = 0006
DASD 019E 3390 LX6W01 R/O 250 CYL ON DASD CD32 SUBCHANNEL = 0007
DASD 0401 3390 LX6W01 R/O 146 CYL ON DASD CD32 SUBCHANNEL = 0009
DASD 0402 3390 LX6W01 R/O 146 CYL ON DASD CD32 SUBCHANNEL = 0008
DASD 0405 3390 LX6W01 R/O 156 CYL ON DASD CD32 SUBCHANNEL = 000A
```

The example displays several different DASD devices available to us. The output shows one DASD device per line. In the first DASD line, the fields have the following meanings:

+   0190 The virtual device number of this DASD device.
+   3390 The type of actual DASD hardware in use.
+   LX6RES The volume label of the real DASD pack label in which this virtual DASD device lives.
+   R/O The level of access you have to the device.
+   107 CYL The size of this DASD device (107) as shown in cylinders (CYL).
+   ON DASD CD31 The real address of the DASD pack that this virtual DASD device resides.
+   SUBCHANNEL = 0005 The subchannel number for our virtual device. A discussion of subchannels is beyond the scope of this book.

The following sections explain the most significant parameters in more detail.

# Virtual device number

As previously mentioned, the virtual device number uniquely identifies this device to your virtual machine. This can be any hexadecimal number that is not already defined to your virtual machine.

# Type

The type used to be important many years ago when there were multiple types of real DASDs. Today, except for the oldest installations, you probably will not see any type of DASD other than 3390. The type parameter is kept in place to