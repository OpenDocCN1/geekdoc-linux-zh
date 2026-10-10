```
```
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
		pmintk(KERN_INFO "cq: unable to get major %d\n", CQ_MAJOR);
		return -EIO;
	}

	cq_area.flags = (CQ_OFF | CQ_EXIST);
	cq_reset();
	return 0;
}
```
```

It is customary to include definitions of parameters used in the C program in an include file. An include file for the Morse Code driver follows.

```
```
#define CQ_EXIST	0x0001
#define CQ_BUSY	0x0002
#define CQ_OFF	0x0004
#define CQ_ABORT	0x0008

/* IOCTL numbers */

#define CQABORT	0x0714
#define CQSETTEMPO	0x0716	/* Store whole note int cq_area. */
#define CQSETPTTCH	0x0719	/* Store a timer divisor into cq_area. */
#define CORESET	0x071c	/* reset speaker */
#define CQGETFLAGS	0x071e	/* get status flags */
```
```