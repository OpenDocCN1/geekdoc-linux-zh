• CMOS driver operations complete synchronously and do not depend on interrupts. However, data access methods belonging to many drivers depend on interrupts for data collection and have to communicate with interrupt context code via data structures such as wait queues.

Listing 5.3 contains the `read()` and `write()` methods belonging to the CMOS driver. You cannot directly access user buffers from kernel space and vice versa, so to copy CMOS memory contents to user space, `cmos_read()` uses the services of `copy_to_user()`. `cmos_write()` does the reverse using `copy_from_user()`. Because `copy_to_user()` and `copy_from_user()` may fall asleep on the job, you cannot hold spinlocks while calling them.

As you saw earlier, accessing CMOS memory is accomplished by operating on a pair of I/O addresses. To read different sizes of data from an I/O address, the kernel provides a family of architecture-independent functions: `in[b|w|l|sb|sl]()`. Similarly, a cluster of routines, `out[b|w|l|sb|sl]()`, are available for writing to I/O regions. `port_data_in()` and `port_data_out()` in Listing 5.3 use `inb()` and `outb()` for data transfer.

# ### Listing 5.3. Read and Write

```
```
Code View:
/*
 * Read from a CMOS Bank at bit-level granularity
 */
ssize_t
cmos_read(struct file *file, char *buf,
          size_t count, loff_t *ppos)
{
    struct cmos_dev *cmos_devp = file->private_data;
    char data[CMOS_BANK_SIZE];
    unsigned char mask;
    int xferred = 0, i = 0, l, zero_out;
    int start_byte = cmos_devp->current_pointer/8;
    int start_bit  = cmos_devp->current_pointer%8;

    if (cmos_devp->current_pointer >= cmos_devp->size) {
        return 0; /*EOF*/
    }

    /* Adjust count if it edges past the end of the CMOS bank */
    if (cmos_devp->current_pointer + count > cmos_devp->size) {
        count = cmos_devp->size - cmos_devp->current_pointer;
    }

    /* Get the specified number of bits from the CMOS */
    while (xferred < count) {
        data[i] = port_data_in(start_byte, cmos_devp->bank_number)
                  >> start_bit;
        xferred += (8 - start_bit);
        if ((start_bit) && (count + start_bit > 8)) {
            data[i] |= (port_data_in (start_byte + 1,
                                      cmos_devp->bank_number) << (8 - start_bit));
            xferred += start_bit;
        }
        start_byte++;
        i++;
    }
    if (xferred > count) {
```

```