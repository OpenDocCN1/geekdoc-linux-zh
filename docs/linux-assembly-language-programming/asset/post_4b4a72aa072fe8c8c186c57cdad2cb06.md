
    time_value = cq_area.wholenote >> 4;
    cq_timer.expires = jiffies + time_value;
    add_timer(&cq_timer);
    speaker_off();
    interruptible_sleep_on(&cq_area.cq_wait_q);
    total_bytes_written = total_bytes_written + copy_size;
    count -= copy_size;
    buf = buf + copy_size;
    } while (count > 0);
    del_timer(&cq_timer);
    return total_bytes_written;
}

static long long cq_lseek(struct file * file,
                          long long offset, int origin)
{
    return -ESPIPE;
}

static int cq_open(struct inode * inode, struct file * file)
{
    unsigned int minor = MINOR(inode->i_rdev);

    if (minor > 0) /* Stereo No */
        return -ENXIO;
    if ((cq_area.flags & CQ_EXIST) == 0)
        return -ENXIO;
    if (cq_area.flags & CQ_BUSY)
        return -EBUSY;

    cq_area.flags = (cq_area.flags | CQ_BUSY);
    return 0;
}

static int cq_release(struct inode * inode, struct file * file)
{
    cq_area.flags = (cq_area.flags &~ CQ_BUSY);
    return 0;
}

static void cq_set_pitch(unsigned long cps)
{
    cq_area.timerdiv = 1193180 / cps;

        /* Frequency of the OSC signal on the AT bus */
}

static void cq_set_tempo(unsigned long beats_per_minute)
{
        /* Quarter note = 1 beat, timer works in centiseconds */

    cq_area.wholenote = 24000 / beats_per_minute;
}

static int cq_ioctl(struct inode *inode, struct file *file,
                    unsigned int cmd, unsigned long arg)
{
    unsigned int minor = MINOR(inode->i_rdev);
    int retval = 0;

    if (minor > 0)
        return -ENODEV;
    if ((cq_area.flags & CQ_EXIST) == 0)
        return -ENODEV;
    switch ( cmd )
    {
    case CQABORT:
        if (arg)
            cq_area.flags = (cq_area.flags | CQ_ABORT);
        else
            cq_area.flags = (cq_area.flags & ~ CQ_ABORT);
        break;
    case CQSETPTTCH:
        if (arg)
            cq_set_pitch(arg);
        else
            retval = -EINVAL;
        break;
    case CQSETTEMPO:
        if (arg)
            cq_set_tempo(arg);
        else
            retval = -EINVAL;
        break;
    case CORESET:
        cq_reset();
        break;
    case CQGETFLAGS:
        retval = verify_area(VERIFY_WRITE,
                    (void *) arg, sizeof(int));
        if (retval)
            return retval;
        else
        {
            int status = cq_area.flags;
            copy_to_user((int *) arg, &status, sizeof(int));
        }
        break;
    default:
        retval = -EINVAL;
    }
    return retval;
}

int cq_init(void)
{
    /* Initialization code like this can be called
       if a call to it is placed in mem.c */
    if (register_chrdev(CQ_MAJOR, "cq" ,&cq_fops))
    {
        printk(KERN_INFO "cq: unable to get major %d\n", CQ_MAJOR);
        return -EIO;
    }

    cq_area.flags = (CQ_OFF | CQ_EXIST);
    cq_reset();
    return 0;
}

It is customary to include definitions of parameters used in the C program in an include file. An include file for the Morse Code driver follows.

#define CQ_EXIST	0x0001
#define CQ_BUSY	0x0002
#define CQ_OFF	0x0004
#define CQ_ABORT	0x0008

/* IOCTL numbers */

#define CQABORT	0x0714
#define CQSETTEMPO	0x0716	/* Store whole note in cq_area. */
#define CQSETPTTCH	0x0719	/* Store a timer divisor into cq_area. */
#define CORESET	0x071c	/* reset speaker */
#define CQGETFLAGS	0x071e	/* get status flags */

#define CQ_BUFFER_SIZE
#define CQ_DEF_CHAR 0 /* Default character */
#define CQ_DEF_PITCH 440 /* Default pitch */
#define CQ_DEF_TEMPO 160 /* Default tempo */
/*
 * function prototypes
 */
extern int cq_init(void);

The functions defined in struct cq_struct take care of the response by the driver to requests that the kernel makes in executing a system call which is asking for service from the driver. The cq_timer_handler() function takes care of the driver's response to a timer interrupt. These are the main things that need to be done. But when the device driver works, commands such as

`linuxbox$ cat file > /dev/cq`

will start the speaker bleeping. In order for this to happen, there has to be an entry named cq in the /dev directory, which has a connection with the programs such as cq_write().

### 11.3.11 Loose Ends

To finish the device driver, it is only necessary to

- Add a major number for the device to the /usr/include/linux/major.h file.
- Create an entry for the device in the /dev directory using the mknod command.
- Write a cq_init() function and include a call to it in the mem.c file.
- Modify the Makefile for the directory containing the driver, in this case /usr/src/linux/drivers/char, and recompile the kernel.

The /dev directory contains a list of a great many files, most of which are not actually files. The ls -1 command distinguishes different types of files in the very first character of each line. Files which really are files are listed beginning with a -, directories are listed with a d, hard links with an l, etc. Devices are listed with either a b or a c, depending on whether they are block devices or character devices. Block devices transfer data in blocks, i.e., big uniformly-sized chunks. To do this, they interact with the kernel's buffer cache. Block devices can be mounted, i.e., incorporated into Unix's tree-structured file hierarchy. A hard drive is a good example of a block device. Character devices don't use blocks and they don't get mounted. Our little speaker driver is a character device. Each device listing, whether for a block or a character device, also lists a major number and a minor number. The major number is used as an index into chrdevs, a kernel array of character device drivers.

`struct device_struct chrdevs[MAX_CHRDEV]`

Each device driver is just a

`struct device_struct {`
`    const char * name;`
`    const struct file_operations * fops;`
`};`

The device is entered into the array by the function register_chrdev() which is defined in /usr/src/linux/fs/devices.c. The most important lines of this definition are as follows.

Program 11.8

`int register_chrdev(unsigned int major, const char * name,`
`                    struct file_operations *fops)`
`{`
`    chrdevs[major].name = name;`
`    chrdevs[major].fops = fops;`
`    return 0;`
`}`

When this function is called, the major number is connected to the file operations structure set up by the device driver. The call is made by the device driver in the cq_init() function. The only other task performed by cq_init() is the initialization of some of the values in cq_area. In order to get the call performed during boot time, a call to it may be placed in the mem.c program near the end near the call to lp_init(). The command

`linuxbox$ mknod /dev/cq c 102 0`

creates an entry in file system for the cq device, giving it a major number of 102 and a minor number of 0. This entry in /dev directory is then used to translate references to /dev/cq into calls to the functions listed in the file operations structure.

## 11.4 Serial Port Digitizer Driver

The Sealex device is a hand-held measuring device for reading distances off of a flat surface. It inputs data at a rate of 600 baud through the serial port. Since it has no handshaking hardware it does not respond to software which treats it as a modem or a terminal. It also handles data in a special format which packs two four-bit characters into each byte sent or received. For both of these reasons it is useful to write a special driver for it.

One important element of a typical device driver, which was not needed in the Morse Code device driver, was the installation of an interrupt handler. The Morse Code driver simply took advantage of the services of the existing interrupt handler for the timer interrupt.

### 11.4.1 Setting Up a New Interrupt Handler

Most device drivers need an ISR to handle interrupts which come from the device. The Linux function request_irq() takes care of the installation of a new handler. Its definition is located in /usr/src/linux/arch/i386/kernel/irq.c.

`int request_irq(unsigned int irq,`

Table 11.1. ASCII Code Chart

|  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|
| 0 | Ctrl-@ | 32 | <SPC> | 64 | @ | 96 | ` |
| 1 | Ctrl-A | 33 | ! | 65 | A | 97 | a |
| 2 | Ctrl-B | 34 | " | 66 | B | 98 | b |
| 3 | Ctrl-C | 35 | # | 67 | C | 99 | c |
| 4 | Ctrl-D | 36 | $ | 68 | D | 100 | d |
| 5 | Ctrl-E | 37 | % | 69 | E | 101 | e |
| 6 | Ctrl-F | 38 | & | 70 | F | 102 | f |
| 7 | Ctrl-G | 39 | ' | 71 | G | 103 | g |
| 8 | Ctrl-H | 40 | ( | 72 | H | 104 | h |
| 9 | Ctrl-I | 41 | ) | 73 | I | 105 | i |
| 10 | Ctrl-J | 42 | * | 74 | J | 106 | j |
| 11 | Ctrl-K | 43 | + | 75 | K | 107 | k |
| 12 | Ctrl-L | 44 | , | 76 | L | 108 | l |
| 13 | Ctrl-M | 45 | - | 77 | M | 109 | m |
| 14 | Ctrl-N | 46 | . | 78 | N | 110 | n |
| 15 | Ctrl-O | 47 | / | 79 | O | 111 | o |
| 16 | Ctrl-P | 48 | 0 | 80 | P | 112 | p |
