Look at `cmos_llseek()` in Listing 5.4 and co-relate with the preceding definitions.

# Listing 5.4. Seek

```
Code View:
```
/*
 * Seek to a bit offset within a CMOS bank
 */
static loff_t
cmos_llseek(struct file *file, loff_t offset,
 int orig)
{
 struct cmos_dev *cmos_devp = file->private_data;

switch (orig) {
case 0; /* SEEK_SET */
 if (offset >= cmos_devp->size) {
 return -EINVAL;
 }
 cmos_devp->current_pointer = offset; /* Bit Offset */
 break;

case 1; /* SEEK_CURR */
 if ((cmos_devp->current_pointer + offset) >=
 cmos_devp->size) {
 return -EINVAL;
 }
 cmos_devp->current_pointer = offset; /* Bit Offset */
 break;

case 2; /* SEEK_END - Not supported */
 return -EINVAL;

default:
 return -EINVAL;
}

return(cmos_devp->current_pointer);
}
```
```

# Control

Another common char driver method is called I/O Control (or *ioctl*). This routine is used to receive and implement application commands that request device-specific actions. Because CMOS memory is used by the BIOS to store crucial information such as the boot device order, it's usually protected via *cyclic redundancy check* (CRC) algorithms. To detect data corruption, the CMOS driver supports two ioctl commands:

+   1. *Adjust checksum*, which is used to recalculate the CRC after the CMOS contents have been modified. The calculated checksum is stored at a predetermined offset in CMOS bank 1.