# 7.2 SLIP Implementation in the Linux Kernel 141

# s1_xmit()

drivers/net/slip.c

This function is invoked by the IP layer, which uses the function pointer hard_start_xmit() of the net_device structure to output an IP packet over the SLIP network device. The actual work is delegated to the function s1_encaps().

# s1_encaps()

drivers/net/slip.c

This function is invoked by s1_xmit(). As explained in section 7.1.1, it converts the IP packet into a byte sequence. Depending on the SLIP operating mode (CSIP, etc.), other functions may be called in addition (e.g., the function slip_esc()). Subsequentially, s1_encaps() invokes the function write() of the underlying TTY driver, which eventually sends the built byte sequence previously created over the TTY device.

# slip_esc()

drivers/net/slip.c

This function is invoked by s1_encaps() and does the character smashing described in Section 7.1.1. A similar function called slip_esc6() exists for the SLIP operating mode SLIP6, which additionally divides the data into 6-bit chunks and converts it into printable characters.

# slip_write_wakeup()

drivers/net/slip.c

This function is invoked by the underlying TTY driver over the function pointer_write_wakeup() of the tty_1ldisc structure (see Section 7.2.1) as soon as the TTY device is ready to accept more data. (Also See Section 7.2.7).

# slip_receive_room()

drivers/net/slip.c

This function is invoked by the underlying TTY driver over the function pointer_receive_room() of the tty_1ldisc structure and simply returns the value 65536, because the SLIP implementation can process a maximum of 65536 bytes per call of slip_receive_buf().

# slip_receive_buf()

drivers/net/slip.c

This function is invoked by the underlying TTY driver to transfer data from the TTY device to the SLIP driver. receive_buf() of the tty_1ldisc structure. The function slip_unesc() (slip_unesc6()), for the SLIP6 operating mode is invoked to convert the incoming byte stream back into IP packets.

# slip_unesc()

drivers/net/slip.c

This function is invoked by slip_receive_buf(): it converts the incoming byte stream into IP packets, using the method described in Section 7.1.1. The function