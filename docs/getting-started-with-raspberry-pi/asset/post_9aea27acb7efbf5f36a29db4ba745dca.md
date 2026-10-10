
are in text mode or *pseudo terminals* (PTYs) if you are in graphics mode. VTs and PTYs are implemented as tty drivers and live in *drivers/char/vt.c* and *drivers/char/pty.c*, respectively.

- The tty driver used over conventional UARTs resides in *drivers/serial/serial_core.c*.
- The USB-serial tty driver is in *drivers/usb/serial/usb-serial.c*.

## Line Disciplines

Line disciplines provide an elegant mechanism that lets you use the same serial driver to run different technologies. The low-level physical driver and the tty driver handle the transfer of data to and from the hardware, while line disciplines are responsible for processing the data and transferring it between kernel space and user space.

The serial subsystem supports 17 standard line disciplines. The default line discipline that gets attached when you open a serial port is N_TTY, which implements terminal I/O processing. N_TTY is responsible for “cooking” characters received from the keyboard. Depending on user request, it maps the control character to newline, converts lowercase to uppercase, expands tabs, and echoes characters to the associated VT. N_TTY also supports a raw mode used by editors, which leaves all the preceding processing to user applications. See Figure 7.3 in the next chapter, “Input Drivers,” to learn how the keyboard subsystem is connected to N_TTY. The example tty drivers listed at the end of the previous section, “TTY Drivers,” use N_TTY by default.

Line disciplines also implement network interfaces over serial transport protocols. For example, line disciplines that are part of the Point-to-Point Protocol (N_PPP) and the Serial Line Internet Protocol (N_SLIP) subsystems, frame packets, allocate and populate associated networking data structures, and pass the data on to the corresponding network protocol stack. Other line disciplines handle Infrared Data (N_IRDA) and the Bluetooth Host Control Interface (N_HCI).

## Device Example: Touch Controller

Let’s take a look at the internals of a line discipline by implementing a simple line discipline for a serial touch-screen controller. Figure 6.6 shows how the touch controller is connected on an embedded laptop derivative. The Finite State Machine (FSM) of the touch controller is a candidate for being implemented as a line discipline because it can leverage the facilities and interfaces offered by the serial layer.

![](img/07cc6f9c8c74622020874f66bfb53dc4_182_0.png)

### Open and Close

To create a line discipline, define a struct tty_ldisc and register a prescribed set of entry points with the kernel. Listing 6.2 contains a code snippet that performs both these operations for the example touch controller.

#### Listing 6.2. Line Discipline Operations

```
struct tty_ldisc n_touch_ldisc = {
    TTY_LDISC_MAGIC,       /* Magic */
    "n_tch",
    N_TCH,                 /* Name of the line discipline */
    /* Line discipline ID number */
    n_touch_open,          /* Open the line discipline */
    n_touch_close,         /* Close the line discipline */
    n_touch_flush_buffer,  /* Flush the line discipline's read buffer */
    n_touch_chars_in_buffer,/* Get the number of processed characters in the line discipline's read buffer */
    n_touch_read,          /* Called when data is requested from user space */
    n_touch_write,         /* Write method */
    n_touch_ioctl,         /* I/O Control commands */
    NULL,                  /* We don't have a set_termios routine */
    n_touch_poll,          /* Poll */
    n_touch_receive_buf,   /* Called by the low-level driver to pass data to user space*/
    n_touch_receive_room,  /* Returns the room left in the line discipline's read buffer */
    n_touch_write_wakeup   /* Called when the low-level device driver is ready to transmit more data */
};
/* ... */
if ((err = tty_register_ldisc(N_TCH, &n_touch_ldisc))) {
    return err;
}
```

In Listing 6.2, n_tch is the name of the line discipline, and N_TCH is the line discipline identifier number. You have to specify the value of N_TCH in include/linux/tty.h, the header file that contains all line discipline definitions. Line disciplines active on your system can be found in /proc/tty/ldiscs.

Line disciplines gather data from their half of the tty flip buffer, process it, and copy the resulting data to a local read buffer. For N_TCH, n_touch_receive_room() returns the memory left in the read buffer, while n_touch_chars_in_buffer() returns the number of processed characters in the read buffer that are ready to be delivered to user space. n_touch_write() and n_touch_write_wakeup() do nothing because N_TCH is a read-only device. n_touch_open() takes care of allocating memory for the main line discipline data structures, as shown in Listing 6.3.

#### Listing 6.3. Opening the Line Discipline

```
/* Private structure used to implement the Finite State Machine
(FSM) for the touch controller. The controller and the processor
communicate using a specific protocol that the FSM implements */
struct n_touch {
  int current_state;    /* Finite State Machine */
  spinlock_t touch_lock; /* Spinlock */
  struct tty_struct *tty; /* Associated tty */
  /* Statistics and other housekeeping */
  /* ... */
} *n_tch;

/* Device open() */
static int
n_touch_open(struct tty_struct *tty)
{
  /* Allocate memory for n_tch */
  if (!(n_tch = kmalloc(sizeof(struct n_touch), GFP_KERNEL))) {
    return -ENOMEM;
  }
  memset(n_tch, 0, sizeof(struct n_touch));

  tty->disc_data = n_tch; /* Other entry points now
                            have direct access to n_tch */
  /* Allocate the line discipline's local read buffer
     used for copying data out of the tty flip buffer */
  tty->read_buf = kmalloc(BUFFER_SIZE, GFP_KERNEL);
  if (!tty->read_buf) return -ENOMEM;

  /* Clear the read buffer */
  memset(tty->read_buf, 0, BUFFER_SIZE);

  /* Initialize lock */
  spin_lock_init(&n_tch->touch_lock);

  /* Initialize other necessary tty fields.
     See drivers/char/n_tty.c for an example */
  /* ... */

  return 0;
}
```

You might want to set `N_TCH` as the default line discipline (rather than `N_TTY`) whenever the serial port connected to the touch controller is opened. See the section "Changing Line Disciplines" to see how to change line disciplines from user space.

## Read Path

For interrupt-driven devices, the read data path usually consists of two threads working in tandem:

1. A top thread originating from the user process requesting the read
2. A bottom thread springing from the interrupt service routine that collects data from the device

Figure 6.7 shows these threads associated with the read data flow. The interrupt handler queues the *receive_buf() method (n_touch_receive_buf() in our example) as a task. You can override this behavior by setting the tty->low_latency flag.

### Figure 6.7. Line discipline read path.

![](img/07cc6f9c8c74622020874f66bfb53dc4_185_0.png)

The touch controller and the processor communicate using a specific protocol described in the controller's data sheet. The driver implements this communication protocol using an FSM as indicated earlier. Listing 6.4 encodes this FSM as part of the *receive_buf()* entry point, n_touch_receive_buf().

### Listing 6.4. The n_touch_receive_buf() Method

```
static void
n_touch_receive_buf(struct tty_struct *tty,
                    const unsigned char *cp, char *fp, int count)
{
    /* Work on the data in the line discipline's half of
     * the flip buffer pointed to by cp */

    /* Implement the Finite State Machine to interpret commands/data
     * arriving from the touch controller and put the processed data
     * into the local read buffer */

    /* Datasheet-dependent Code Region */
    switch (tty->disc_data->current_state) {
    case RESET:
        /* Issue a reset command to the controller */
        tty->driver->write(tty, 0, mode_stream_command,
                           sizeof(mode_stream_command));
        tty->disc_data->current_state = STREAM_DATA;
        break;
    case STREAM_DATA:
        break;
    case PARSING:
        tty->disc_data->current_state = PARSED;
        break;
    case PARSED:
        break;
    }

    if (tty->disc_data->current_state == PARSED) {
        /* If you have a parsed packet, copy the collected coordinate
         * and direction information into the local read buffer */
        spin_lock_irqsave(&tty->disc_data->touch_lock, flags);
        for (i=0; i < PACKET_SIZE; i++) {
            tty->disc_data->read_buf[tty->disc_data->read_head] =
                tty->disc_data->current_pkt[i];
            tty->disc_data->read_head =
                (tty->disc_data->read_head + 1) & (BUFFER_SIZE - 1);
            tty->disc_data->read_cnt++;
        }
        spin_lock_irqrestore(&tty->disc_data->touch_lock, flags);
    }
}
```

n_touch_receive_buf() processes the data arriving from the serial driver. It exchanges a series of commands and responses with the touch controller and puts the received coordinate and direction (press/release)
