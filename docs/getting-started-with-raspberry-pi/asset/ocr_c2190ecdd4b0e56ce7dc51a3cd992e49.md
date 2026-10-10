```
/* Parport attach method */
static void
led_attach(struct parport *port)
{
    /* Register the paralell LED device with parport */
    pdev = parport_register_device(port, DEVICE_NAME,
                     led_preempt, NULL,
                     NULL, 0, NULL);
    if (pdev == NULL) printk("Bad register\n");
}

/* Parport detach method */
static void
led_detach(struct parport *port)
{
    /* Do nothing */
}

/* Parport driver operations */
static struct parport_driver led_driver = {
    .name   = "led",
    .attach = led_attach,
    .detach = led_detach,
};

/* Driver Initialization */
int __init
led_init(void)
{
    /* Request dynamic allocation of a device major number */
    if (alloc_chrdev_region(&dev_number, 0, 1, DEVICE_NAME)
               < 0) {
         printk(KERN_DEBUG "Can't register device\n");
         return -1;
    }

    /* Create the led class */
    led_class = class_create(THIS_MODULE, DEVICE_NAME);
    if (IS_ERR(led_class)) printk("Bad class create\n");

    /* Connect the file operations with the cdev */
    cdev_init(&led_cdev, &led_fops);

    led_cdev.owner = THIS_MODULE;

    /* Connect the major/minor number to the cdev */
    if (cdev_add(&led_cdev, dev_number, 1)) {
         printk("Bad cdev add\n");
         return 1;
    }

    class_device_create(led_class, NULL, dev_number,
                       NULL, DEVICE_NAME);

    /* Register this driver with parport */
    if (parport_register_driver(&led_driver)) {
         printk(KERN_ERR "Bad Parport Register\n");
         return -EIO;
    }
}
```