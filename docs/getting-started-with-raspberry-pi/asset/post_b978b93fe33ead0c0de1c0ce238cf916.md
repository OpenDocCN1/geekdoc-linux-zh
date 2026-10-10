
# User Mode SCSI

The SCSI Generic (sg) interface lets you directly dispatch SCSI commands from user space. The sg driver essentially exports a char interface, so applications can use the open(), close(), read(), write(), ioctl(), poll(), fcntl(), and mmap() system calls to talk to the underlying device. Drivers for SCSI devices such as CD burners and scanners are implemented in user space over sg. Look at the sources of cdtools (previously called cdrrecord) available from http://freshmeat.net/projects/cdrecord/ for a real-life sg user.

Let's learn how to use the sg interface with the help of an example. Listing 19.5 implements a user program that sends a READ_CAPACITY SCSI command to a storage device, such as a SCSI hard disk or a USB mass storage drive to glean its data capacity. The READ_CAPACITY command consists of 10 bytes, starting with the command code 0x25. For the purpose of this example, let's set the rest of the bytes to zero. When a SCSI device receives a READ_CAPACITY command, it responds with an 8-byte reply: the top 4 bytes contain the address of the last logical block, and the bottom 4 bytes contain the block length.

sg device nodes are named /dev/sgX, where X is the device number, so Listing 19.5 opens /dev/sg0, which is assumed to be the sg char node corresponding to your SCSI storage device. It then sets about populating the sg_io_hdr_t structure, which is the main data structure that sg users have to manage. The read(), write(), and ioctl() calls expect a pointer to this structure (defined in /usr/include/scsi/sg.h) as an argument. The cmdp field of sg_io_hdr_t is set to the address of the command block that holds the 10-byte READ_CAPACITY command. The dxf field supplies the address of a buffer that will carry the response data arriving from the device. The dxp field contains the address of a sense buffer that will return the status of the requested operation. The interface_id has to be set to S, and timeout holds the wait time in milliseconds before sg gives up on the command.

SG_IO is an oft-used ioctl command supported by sg. Internally, it writes a command to the device, waits for a response, and reads the received reply into a user-supplied buffer. In Listing 19.5, SG_IO issues a READ_CAPACITY command and reads the 8-byte response into rcap_buff[]. The program calculates and prints the disk capacity by interpreting the data in rcap_buff[].

## Listing 19.5. Obtaining Disk Capacity via SCSI Generic

```c
#include <stdio.h>
#include <fcntl.h>
#include <sys/ioctl.h>
#include <scsi/sg.h>

#define RCAP_COMMAND    0x25
#define RCAP_COMMAND_LEN 10
#define RCAP_REPLY_LEN  8

int
main(int argc, char *argv[])
{
    int fd, i;
    /* READ_CAPACITY command block */
    unsigned char RCAP_CmdBlk[RCAP_COMMAND_LEN] =
                        {RCAP_COMMAND, 0,0,0,0,0,0,0,0,0};
    sg_io_hdr_t sg_io;
    unsigned char rcap_buff[RCAP_REPLY_LEN];
    unsigned int lastblock, blocksize;
    unsigned long long disk_cap;
    unsigned char sense_buf[32];

    /* Open the sg device */
    if ((fd = open("/dev/sg0", O_RDONLY)) < 0) {
        printf("Bad Open\n");
        exit(1);
    }

    /* Initialize */
    memset(&sg_io, 0, sizeof(sg_io_hdr_t));

    /* Command block address and length */
    sg_io.cmdp = RCAP_CmdBlk;
    sg_io.cmd_len = RCAP_COMMAND_LEN;

    /* Response buffer address and length */
    sg_io.dxp = rcap_buff;
    sg_io.dxfer_len = RCAP_REPLY_LEN;

    /* Sense buffer address and length */
    sg_io.sbp = sense_buf;
    sg_io.mx_sb_len = sizeof(sense_buf);

    /* Control information */
    sg_io.interface_id = 'S';
    sg_io.dxfer_direction = SG_DXFER_FROM_DEV;
    sg_io.timeout = 10000; /* 10 seconds */

    /* Issue the SG_IO ioctl */
    if (ioctl(fd, SG_IO, &sg_io) < 0) {
        printf("Bad SG_IO\n");
        exit(1);
    }

    /* Obtain results */
    if ((sg_io.info & SG_INFO_OK_MASK) == SG_INFO_OK) {
        /* Address of last disk block */
        lastblock = ((rcap_buff[0]<<24) | (rcap_buff[1]<<16) |
                     (rcap_buff[2]<<8) | (rcap_buff[3]));
        /* Block size */
        blocksize = ((rcap_buff[4]<<24) | (rcap_buff[5]<<16) |
                     (rcap_buff[6]<<8) | (rcap_buff[7]));
        /* Calculate disk capacity */
        disk_cap = (lastblock+1);
        disk_cap *= blocksize;
        printf("Disk Capacity = %llu Bytes\n", disk_cap);
    }
    close(fd);
}
```

For the full list of SG_IO commands, take a look at *include/scsi/scsi.h* and *drivers/scsi/sg.c*. Read the Linux SCSI Generic HOWTO for an in-depth explanation of the sg interface. Download the *sg3_utils* package from http://sg.torque.net/sg/sg3_utils.html and browse the sources to find several useful programs that operate over sg.

# User Mode USB

The `usbfs` virtual filesystem allows raw access to USB devices from user space. `Usbfs` is usually mounted over `/proc/bus/usb/`. The usbfs tree contains directories corresponding to each USB controller (or bus) on your system. Each of these directories, in turn, contains nodes corresponding to USB devices present on that bus.

To better understand usbfs, let's look at a system with an Intel ICH4 South Bridge chipset. As you learned in Chapter 11, "Universal Serial Bus," USB controllers are part of the South Bridge chipset on PC systems. The ICH4 supports one USB EHCI (high-speed USB 2.0) controller and three USB UHCI controllers and can connect to six physical USB ports. The EHCI controller can converse with all six ports, and the three UHCI controllers can talk to two ports each. Let's call the EHCI controller *bus*1 and the three UHCI controllers *bus*2, *bus*3, and *bus*4, respectively. Now assume that the system has only two physical USB ports and that they are connected to the UHCI controller corresponding to *bus*3. (The $\rightarrow$ symbol attaches comments to command output.)

```bash
bash> ls -1R /proc/bus/usb
```

/proc/bus/usb:
total 0
dr-xr-xr-x   2 root     root      0 Dec  2 12:44 001   $\rightarrow$ EHCI. Can talk to any physical port
dr-xr-xr-x   2 root     root      0 Dec  2 12:44 002   $\rightarrow$ No corresponding physical ports
dr-xr-xr-x   2 root     root      0 Dec  2 12:44 003   $\rightarrow$ UHCI bus for the 2 physical USB ports on this system
dr-xr-xr-x   2 root     root      0 Dec  2 12:44 004   $\rightarrow$ No corresponding physical ports
-r--r--r--   1 root     root      0 Dec  2 20:02 devices

/proc/bus/usb/001:
total 0
-rw-r--r--   1 root     root     43 Dec  2 12:44 001   $\rightarrow$ Root Hub (bus1)

/proc/bus/usb/002:
total 0
-rw-r--r--   1 root     root     43 Dec  2 12:44 001   $\rightarrow$ Root Hub (bus2)

/proc/bus/usb/003:
total 0
-rw-r--r--   1 root     root     43 Dec  2 12:44 001   $\rightarrow$ Root Hub (bus3)

/proc/bus/usb/004:
total 0
-rw-r--r--   1 root     root     43 Dec  2 12:44 001   $\rightarrow$ Root Hub (bus4)

Let's connect a full-speed Nikon digital camera and a high-speed Seagate USB 2.0 hard disk to the two USB ports on the system. First, take a peek at `/proc/bus/usb/devices` and find the relevant entries:

```bash
bash> ls -1R /proc/bus/usb/devices
```
