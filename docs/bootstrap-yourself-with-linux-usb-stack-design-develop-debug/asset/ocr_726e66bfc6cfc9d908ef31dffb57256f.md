```
struct r8a66597 {
    spinlock_t lock;
    unsigned long reg;
    struct r8a66597_platdata *pdata;

    struct usb_gadget gadget;
    struct usb_gadget_driver;
    struct r8a66597_ep ep[R8a66597_MAX_NUM_PIPE];
    struct r8a66597_ep *pipenum2ep[R8a66597_MAX_NUM_PIPE];
    struct r8a66597_ep *epaddr2ep[16];
    struct timer_list;
    struct usb_request *ep0_req; /* for internal request */
    u16 ep0_data; /* for internal request */
    u16 old_vbus;
    u16 scount;
    u16 old_dvsq;

    unsigned char bulk;
    unsigned char interrupt;
    unsigned char isochronous;
    unsigned char num_dma;

    unsigned irq_sense_low:1;
};
```

The next step in the process is to register the device to the Linux platform. This is specific to the way the device controller is connected to the platform. As discussed in the previous section, when the devices are connected to the platform using previous proprietary connections like General Purpose Input/Output (GPIO), the driver is based on platform driver framework. You will also see Peripheral Component Interconnect (PCI) driver framework–based drivers in the drivers/usb/gadget folder. Thus, this declaration is specific to the way the device controller is interfaced to the platform.

In this example setup, the device controller requires a platform driver framework, and the driver declares a struct platform_driver–based object r8a6657_driver. The r8a6657_driver is named to help you easily identify the device and driver when loaded.