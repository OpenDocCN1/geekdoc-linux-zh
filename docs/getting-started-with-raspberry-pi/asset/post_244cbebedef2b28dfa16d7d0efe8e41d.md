
/* Traverse all requested sectors, byte by byte */
for (i = 0; i < 512*req->nr_sectors; i++) {
    /* Wait until the disk is ready. Busy duration should be
       in the order of microseconds. Sitting in a tight loop
       for simplicity; more intelligence required in the real
       world */
    while ((status = inb(STATUS_REGISTER)) & BUSY_STATUS);

    /* Write data to disk from the buffer associated with the
       request */
    outb(req->buffer[i], DATA_REGISTER);
}
good = 1;
break;
}
}
end_request(req, good);
}

## Advanced Topics

Unlike our sample storage driver that transfers data byte by byte, performance-sensitive block drivers rely on DMA for data transfer. Consider, for example, the request() method of the disk array driver for Compaq SMART2 controllers drivers/block/cpqarray.c reproduced here from the 2.6.23.1 kernel sources:

```c
static void do_ida_request(struct request_queue *q)
{
    struct request *creq;
    struct scatterlist tmp_sg[SG_MAX];
    cmdlist_t *c;
    ctrl_info_t *h = q->queuedata;
    int seg;

    /* ... */
    creq = elv_next_request(q);
    /* ... */
    c->rq = creq;
    seg = blk_rq_map_sg(q, creq, tmp_sg);
    /* ... */
    for (i=0; i<seg; i++)
    {
        c->req.sg[i].size = tmp_sg[i].length;
        c->req.sg[i].addr = (_u32) pci_map_page(h->pci_dev,
            tmp_sg[i].page,
            tmp_sg[i].offset,
            tmp_sg[i].length, dir);
    }
    /* ... */
}
```

DMA operations work at bio level. As you saw earlier, I/O requests are made up of bios, each of which contains an array of bio_vecs, which in turn hold information about the constituent memory pages. Assuming that bio points to the bio structure associated with an I/O request, bio->bi_sector contains the starting sector from which data access is requested, bio_cur_sectors(bio) returns the number of sectors on which I/O is to be performed, and bio_data_dir(bio) provides the direction of data transfer. The addresses of the physical pages associated with the data buffer are described by the array of bio_vecs pointed to by bio->bi_io_vec. To iterate over each bio in a request, you can use the rq_for_each_bio() macro. To further loop through each page segment in a bio, use bio_for_each_segment().

In the preceding code snippet, blk_rq_map_sg() internally invokes rq_for_each_bio() and bio_for_each_segment() to loop through all pages constituting the request and builds a scatter/gather list, tmp_sg. Streaming DMA mappings for each page in the created scatter/gather list is performed by pci_map_page().

Unlike our sample driver that busy-waits for requested operations to finish, the cpqarray driver implements an interrupt handler, do_ida_intr(), to receive alerts from the hardware upon completion of commands.

Some drivers, such as the ramdisk driver (drivers/block/rd.c) and the loopback driver (drivers/block/loop.c), work over virtual block devices that do not benefit from the optimizing sort and merge operations on the request queue. Such drivers entirely bypass the request queue and directly obtain bios from the block layer using a make_request() function. So, instead of registering a request queue handler using blk_init_queue(), drivers/block/rd.c supplies a make_request() routine using blk_queue_make_request() as follows:

```c
static int __init rd_init(void)
{
    /* ... */
    blk_queue_make_request(rd_queue[i], &rd_make_request);
    /* ... */
}

static int rd_make_request(struct request_queue *q, struct bio *bio)
{
    /* ... */
}
```

## Debugging

The hdparm utility elicits various PATA/SATA disk parameters from the underlying kernel driver. To benchmark disk read speeds on a SATA drive, for example, do this:

```bash
bash> hdparm -T -t /dev/sda
/dev/sda:
  Timing cached reads:   2564 MB in  2.00 seconds = 1283.57 MB/sec
  Timing buffered disk reads:  132 MB in  3.03 seconds =  43.61 MB/sec
```

For the full capabilities of hdparm, read the man pages.

*Self-Monitoring, Analysis, and Reporting Technology* (SMART) is a system built in to many modern ATA and SCSI disks to monitor failures and perform self-tests. A user-space daemon named smartd collects the information gathered by SMART-capable disks with the help of the underlying device driver. Look at the man pages of smartd, smartctl, and smartd.conf to learn how to obtain health status from SMART-enabled disks.

If your distribution doesn't prepackage hdparm and SMART tools, you may download them from http://sourceforge.net/projects/hdparm/ and http://sourceforge.net/projects/smartmontools/, respectively.

Files under /proc/ide/ contain information about IDE disk drives on your system. To obtain the geometry of the first IDE disk, for example, look at the contents of /proc/ide/ide0/hda/geometry. Information pertaining to SCSI devices is available under /proc/scsi/. You can gather disk partition information from /proc/partitions.

The sysfs directory of interest for IDE devices is /sys/bus/ide/ and for SCSI is /sys/bus/scsi/. In addition, each block device active on the system owns a subdirectory under /sys/block/, which contains associated request queue parameters, constituent partition details, and state information.

Some kernel configuration options are available that trigger the emission of debug output from the block subsystem. CONFIG_BLK_DEV_IO_TRACE provides the ability to trace the block layer. CONFIG_SCSI_CONSTANTS and CONFIG_SCSI_LOGGING turn on SCSI error reporting and logging, respectively.

The linux-ide mailing list is the forum to discuss questions related to the Linux-IDE subsystem. Subscribe to the linux-scsi mailing list and browse through its archives for discussions pertaining to the Linux-SCSI subsystem.

## Looking at the Sources

Table 14.1 contains the location of kernel driver sources for various storage technologies. Take a look at Documentation/ide.txt, Documentation/scsi/*, and Documentation/cdrom/ for information about associated storage drivers.

The top-level block/ directory contains I/O scheduling algorithms and the block core layer. Table 14.2 lists the source files in this directory that implement various I/O schedulers. Look at Documentation/block/ for related documentation.

Table 14.4 contains the main data structures used in this chapter and their location in the source tree. Table 14.5 lists the main kernel programming interfaces that you used in this chapter, along with the location of their definitions.

| Data Structure | Location | Description |
|---|---|---|
| gendisk | include/linux/genhd.h | Representation of a disk. |
| request_queue | include/linux/blkdev.h | The I/O request queue associated with a gendisk. |
| request | include/linux/blkdev.h | Each request in a request_queue is described using this structure. |
| block_device_operations | include/linux/fs.h | Block device driver methods. |
| bio | include/linux/bio.h | Low-level description of block I/O operations. |

| Kernel Interface | Location | Description |
|---|---|---|
| register_blkdev() | block/genhd.c | Registers a block driver with the kernel |
| unregister_blkdev() | block/genhd.c | Unregisters a block driver from the kernel |
| alloc_disk() | block/genhd.c | Allocates a gendisk |
| add_disk() | block/genhd.c | Adds a populated gendisk to the kernel block layer |
| del_gendisk() | fs/partitions/check.c | Frees a gendisk |
| blk_init_queue() | block/ll_rw_blk.c | Allocates a request_queue and registers a request() function to process the requests in the queue |
| blk_cleanup_queue() | block/ll_rw_blk.c | Reverse of blk_init_queue() |
| blk_queue_make_request() | block/ll_rw_blk.c | Registers a make_request() function, which bypasses the request queue and directly obtains requests from the block layer |
| rq_for_each_bio() | include/linux/blkdev.h | Iterates over each bio in a request |
| bio_for_each_segment() | include/linux/bio.h | Loops through each page segment in a bio |
| blk_rq_map_sg() | block/ll_rw_blk.c | Iterates through the bio segments constituting a request and builds a scatter/gather list |
| blk_queue_max_sectors() | block/ll_rw_blk.c | Sets the maximum sectors for a request in the associated request queue |
| blk_queue_hardsect_size() | block/ll_rw_blk.c | Sector size supported by the storage hardware. |
| set_capacity() | include/linux/genhd.h | Sets the capacity of the storage media in terms of number of sectors |
| blk_fs_request() | include/linux/blkdev.h | Checks whether a request obtained from the request queue is a filesystem request |
| elv_next_request() | block/elevator.c | Obtains the next entry from the request queue |
| end_request() | block/ll_rw_blk.c | Ends I/O on a request |

