# # User Mode SCSI

The SCSI Generic (sg) interface lets you directly dispatch SCSI commands from user space. The sg driver essentially exports a char interface, so applications can use the open(), close(), read(), write(), ioctl(), poll(), fcntl(), and mmap() system calls to talk to the underlying device. Drivers for SCSI devices such as CD burners and scanners are implemented in user space over sg. Look at the sources of cdtools (previously called cdrrecord) available from http://freshmeat.net/projects/cdrecord/ for a real-life sg user.

Let's learn how to use the sg interface with the help of an example. Listing 19.5 implements a user program that sends a READ_CAPACITY SCSI command to a storage device, such as a SCSI hard disk or a USB mass storage drive to glean its data capacity. The READ_CAPACITY command consists of 10 bytes, starting with the command code 0x25. For the purpose of this example, let's set the rest of the bytes to zero. When a SCSI device receives a READ_CAPACITY command, it responds with an 8-byte reply: the top 4 bytes contain the address of the last logical block, and the bottom 4 bytes contain the block length.

sg device nodes are named /dev/sgX, where X is the device number, so Listing 19.5 opens /dev/sg0, which is assumed to be the sg char node corresponding to your SCSI storage device. It then sets about populating the sg_io_hdr_t structure, which is the main data structure that sg users have to manage. The read(), write(), and ioctl() calls expect a pointer to this structure (defined in /usr/include/scsi/sg.h) as an argument. The cmdp field of sg_io_hdr_t is set to the address of the command block that holds the 10-byte READ_CAPACITY command. The dxf field field supplies the address of a buffer that will carry the response data arriving from the device. The dxp field contains the address of a sense buffer that will return the status of the requested operation. The interface_id has to be set to S, and timeout holds the wait time in milliseconds before sg gives up on the command.

SG_IO is an oft-used ioctl command supported by sg. Internally, it writes a command to the device, waits for a response, and reads the received reply into a user-supplied buffer. In Listing 19.5, SG_IO issues a READ_CAPACITY command and reads the 8-byte response into rcap_buff[]. The program calculates and prints the disk capacity by interpreting the data in rcap_buff[].

# Listing 19.5. Obtaining Disk Capacity via SCSI Generic

```
Code View:
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
```