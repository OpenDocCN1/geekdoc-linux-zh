```
mask = 1 << start_bit;
end_l = 8;
if ((count-xferred) < (8 - start_bit)) {
    end_l = (count - xferred) + start_bit;
}

for (l = start_bit; l < end_l; l++) {
    tmp_data &= ~mask; mask <<= 1;
}
tmp_kbuf = kbuf[i];
mask = 1 << end_l;
for (l = end_l; l < 8; l++) {
    tmp_kbuf &= ~mask;
    mask <<= 1;
}

port_data_out(start_byte,
               tmp_data | (tmp_kbuf << start_bit),
               cmos_devp->bank_number);
xferred += (end_l - start_bit);

if ((xferred < count) && (start_bit) &&
    (count + start_bit > 8)) {
    tmp_data = port_data_in(start_byte+1,
                            cmos_devp->bank_number);
    start_l = ((start_bit + count) % 8);
    mask = 1 << start_l;
    for (l=0; l < start_l; l++) {
        mask >>= 1;
        tmp_data &= ~mask;
    }
    port_data_out((start_byte+1),
                  tmp_data | (kbuf[i] >> (8 - start_bit)),
                  cmos_devp->bank_number);
    xferred += start_l;
}

start_byte++;
i++;

if (!xferred) return -EIO;
/* Push the offset pointer forward */
cmos_devp->current_pointer += xferred;
return xferred; /* Return the number of written bits */
}

/*
 * Read data from specified CMOS bank
 */
unsigned char
port_data_in(unsigned char offset, int bank)
{
    unsigned char data;

    if (unlikely(bank >= NUM_CMOS_BANKS)) {
        printk("Unknown CMOS Bank\n");
```