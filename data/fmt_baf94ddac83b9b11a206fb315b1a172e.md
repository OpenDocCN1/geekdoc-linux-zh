
# Scalex 驱动代码

```c
static ssize_t scalex_write(struct file * file, const char * buf,
size_t count, loff_t *ppos)
{
ssize_t retv;
unsigned long copy_size;
int j, k, lsr_reg;
char c, d;
struct scalex_struct *scalex = &scalex_area;

/* Scalex takes short command strings.
Characters following termination will be discarded.
Termination will be added to all strings.
*/

k = 0;
while (buf [k] != 0 && k < SCALEX_WRITE_SIZE &&
k < count) k = k + 1;

if ( k == SCALEX_WRITE_SIZE)
return -EINVAL;
if (k == 0) return count;

/* Since count <= SCALEX_WRITE_BUFSIZE */
copy_size = k;
for(k = 0; k < copy_size; k = k + 1)
{
    c = buf[k];
    if(!ok_ascii_char(c))
        return -EFAULT;
}

if (copy_from_user(scalex->write_buffer, buf, copy_size))
{
    return -EFAULT;
}

k = copy_size;
/* Pack each two bytes from the user's buffer into one byte
of the scalex buffer.  */
for(k = 0, j = 0; k <= copy_size; k = k + 2, j = j + 1)
    if (k == copy_size)
    {
        scalex->write_buffer[j] = 0xfd;
    }
    else if (k + 1 == copy_size)
    {
        c = cut (buf [k]);
        scalex->write_buffer[j] = (0xd0 | c);
    }
    else
    {
        c = cut(buf[k]);
        d = cut(buf[k+1]) << 4;
        scalex->write_buffer[j] = (d|c);
    }

scalex->wretein = j; /* Number of bytes into scalex buffer */
while(!(inh_p(SCALEX_COM_BASE + 5) & SCALEX_LSR_DATA_OUT_EMPTY));
scalex->wretein = 1; /* Next byte to be transmitted */
lsr_reg = inh_p(SCALEX_COM_BASE + 5);
if (lsr_reg & 1)
{
    /* Read this damn byte. It shouldn't be here but it is.  */
    c = inh_p(SCALEX_COM_BASE);
    d = char_fill(c & 0xf);

    if (((scalex -> readout == /* Circular buffer is full. */
    ((scalex -> readin + 1) % SCALEX_READ_BUFFER_SIZE)))||
    ((scalex -> readout ==
    ((scalex -> readin + 2) % SCALEX_READ_BUFFER_SIZE)))
    {
        scalex -> flags =
        (scalex -> flags | SCALEX_ERR | SCALEX_RFULL);
        printk("The read buffer overflowed!\n");
        return -EFAULT;
    }
    if (d == 0) /* Other half byte should be just filler. */
    {
        /* Don't store this. It might get the read stuck. */
    }
    else
    {
        scalex -> read_buffer[scalex -> readin] = d;
        scalex -> readin =
        ((scalex -> readin + 1) % SCALEX_READ_BUFFER_SIZE);
    }

    d = char_fill (c >> 4);  
    if (d == 0)
    {
        /* Don't store this either. */
    }
    else
    {
        scalex -> read_buffer [scalex -> readin] = d;
        scalex -> readin =
            ((scalex -> readin + 1) % SCALEX_READ_BUFFER_SIZE);
    }
}

outb_p(scalex->write_buffer[0], SCALEX_COM_BASE );
interruptible_sleep_on(&scalex->rwait_g);
if (signal_pending(current))
    return -EINTR;
retv = count;
return retv;
}

static long long scalex_lseek(struct file * file,
            long long offset, int origin)
{
    return -ESPIPE;
}

static ssize_t scalex_read(struct file * file, char * buf,
       size_t length, loff_t *pos)
{
    struct scalex_struct * scalex = &scalex_area;
    ssize_t count_;
    int k = 0;
    /*
     Read from ascii_read buffer.
     Make the interrupt handler do the translating.
     see if char is waiting in buffer
     if so read it.
     if not set READ_PENDING bit and go to sleep
     */
    scalex->flags = (scalex->flags | SCALEX_RPEND);
    count = length;
    do
    {
        if(scalex->readin == scalex->readout)
            interruptible_sleep_on(&scalex->rdwait_g);
        if(scalex->readin != scalex->readout)
        {
            buf[k] = scalex->read_buffer [ scalex->readout];
            scalex->readout
                = (scalex->readout + 1) % SCALEX_READ_BUFFER_SIZE;
                k = k + 1;
            if (buf [k -1] == SCALEX_READ_STRING_TERMINAL)
                return k;
            /*
            Whether the TERMINAL string is counted as one of the bytes read
            or not has a drastic effect.  Scan hangs on EOLs if it is
            but on ordinary strings if it is not.
            It is probably better to count it.
            */
        }
        count = count - 1;
    } while(count > 0);
    count = k;
    /* Interrupt handler should check READ_PENDING bit
       and issue a wake up if its set. */
    scalex->flags = (scalex->flags & ~SCALEX_RPEND);
    return count;
}

static int scalex_open(struct inode * inode, struct file * file)
{
  char c;
if ((scalex_area.flags & SCALEX_EXIST) == 0)
    return -ENXIO;
if (scalex_area.flags & SCALEX_BUSY)
    return -EBUSY;

scalex_area.read_buffer =
  (char *) kmalloc(SCALEX_READ_BUFFER_SIZE, GFP_KERNEL);

scalex_area.write_buffer =
  (char *) kmalloc(SCALEX_WRITE_BUFFER_SIZE, GFP_KERNEL);
if (!scalex_area.read_buffer || !scalex_area.write_buffer)
{
  scalex_area.flags = (scalex_area.flags | SCALEX_BUSY);
  return -ENOMEM;
}
/*
Initialize the Scalex Area
*/
scalex_area.readin = 0;
scalex_area.readout = 0;
scalex_area.writein = 0;
scalex_area.writeout = 0;

/*
Initialize the COM port
*/

c = inb_p(SCALEX_COM_BASE + 3); /* Line Control Register.  */
c = c | 0x80; /* Bit 7 allows Baud Rate Setting */
outb_p(c, SCALEX_COM_BASE + 3);
outb_p(0, SCALEX_COM_BASE + 1); /* Baud Rate Divisor,Upper Byte */
outb_p(0xc0, SCALEX_COM_BASE); /* 600 Baud, BRD, Lower Byte */
outb_p(3, SCALEX_COM_BASE + 3);
          /* Put back bit 7 and make parity 8,N,1 */
c = inb_p(SCALEX_COM_BASE + 4); /* modem Control Register */

outb_p(3, SCALEX_COM_BASE +1);  /* Interrupt Enable Register */
/* Transmit and Receive Ready Only */
c = (c | 8);
outb_p(c, SCALEX_COM_BASE + 4); /* Enable interrupts */

return 0;
}

static int scalex_release(struct inode * inode, struct file * file)
{
  unsigned int minor = MINOR(inode->i_rdev);
char c;

if (minor > 0)
    return -ENODEV;

kfree_s(scalex_area.read_buffer, SCALEX_READ_BUFFER_SIZE);
kfree_s(scalex_area.write_buffer, SCALEX_WRITE_BUFFER_SIZE);
scalex_area.read_buffer = NULL;
scalex_area.write_buffer = NULL;
scalex_area.flags = (scalex_area.flags & ~SCALEX_BUSY);
c = inb_p(SCALEX_COM_BASE + 4); /* Disable interrupts */
c = (c & ~0xff);
outb_p(c, SCALEX_COM_BASE + 4);
return 0;
}

static int scalex_ioctl(struct inode *inode, struct file *file,
		unsigned int cmd, unsigned long arg)
{
	unsigned int minor = MINOR(inode->i_rdev);
	int status;
	int retval = 0;

	if (minor > 0)
		return -ENODEV;
	if ((scalex_area.flags & SCALEX_EXIST) == 0)
		return -ENODEV;
	switch ( cmd ) {
	case SCALEXRESET:
		scalex_reset();
		break;
	case SCALEXGETFLAGS:
		status = scalex_area.flags ;
		if (copy_to_user((int *) arg, &status, sizeof(int)))
		return -EFAULT;
		break;
	default:
		retval = -EINVAL;
	}
	return retval;
}

static struct file_operations scalex_fops ={
	scalex_lseek,
	scalex_read,
	scalex_write,
	NULL, /* scalex readdir */
	NULL, /* scalex_poll */
	scalex_ioctl,
	NULL, /* scalex_mmap */
	scalex_open,
	NULL, /* flush */
	scalex_release
};

int scalex_init(void)
{
	if (register_chrdev(SCALEX_MAJOR, "scalex", &scalex_fops))
	{
		printk("scalex: unable to get major %d\n", SCALEX_MAJOR);
		return -EIO;
	}
	if (request_irq(4, scalex_interrupt, 0, "scalex", NULL))
	{
		printk("scalex: unable to get irq %d\n", 4);
		return -EIO;
	}
	scalex_area.flags = SCALEX_EXIST;
	return 0;
}
```
