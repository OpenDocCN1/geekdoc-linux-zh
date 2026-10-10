# 182 Chap. 3 vpmem, vpreload, vparboot, PDC, ISL, hpxuc, Secure Web Console, GSP Configuration

# Booting To Simple User Mode

In this example, the -i option is used to make the system come up in run-level 5, for single user mode of operation.

ISL: hpxux -2i

Boot

: disc(8.0.0;0x0;/stand/vmunix
9e6616+397312+409688 start 0xc650

# Kernel Startup Messages Omitted

INIT: Overriding default level with level 'a'

INIT: SINGLE USER MODE
WARNING: YOU ARE SUPERUSER!!

#

# Booting With A Modified I/O Configuration

Here, a tape driver is configured in at CIO slot 2, HP-IB address 0.
Regardless of what was present in the kernel's original I/O
configuration, the driver tape is now configured at that hardware
path. Similarly, mux0 is configured in at CIO slot 1, which is to be
the console. The only other devices configured are the console and
root device, which boot derived from pdc.

ISL: hpxux -sc mux0(8.1) -a tape(8.2.0)

Boot

: disc(8.0.0;0x0;/stand/vmunix
: Adding mux0(8.1;0x0)...
: Adding tape(8.2.0;0x0)...
9e6616+397312+409688 start 0xc650
Beginning I/O System Configuration.
cio-cd address = 8
hpioa address = 0
disc0 lu = 0 address = 0
mux0 lu = 0 address = 1
hpiao address = 2
tape0 lu = 0 address = 0
I/O System Configuration complete.

Additional Kernel Startup Messages Omitted

# Booting From A Raw Device

This example shows booting from a raw device (that is, a device
containing no file system). Note that no file name is specified in the
devicefile. The device is an SBT4374 tape drive, and therefore
tape is the manager used. The tape drive is at CIO slot 2, HP-IB
address 3. The first file on the tape will be skipped. The minor
number specifies a tape density of 1600 BPI with no rewind on close.
Depending on the minor number, tape requires the tape be written with
512 or 1024 byte blocks.

ISL> hpxux tape(8.2.3;0xa0000)

Boot

: tape(8.2.3;0xa0000)
9e6616+397312+409688 start 0xc650

# Displaying The Autoexecute File

In this example, show autofile is used to print the contents of the
autoexecute file residing in the boot LIF, on the device from which
hpxux was booted. Optionally, a devicefile can be specified in order
to read the autoexecute file from the boot LIF of another boot device.