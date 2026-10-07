# USB Monitor: usbmon 26

handlers for usb_mon_operations using the usb_mon_register interface function exported by the usbcore. This callback gives access to URB operations such as submit, complete, and submit error to the usbmon infrastructure.

```
struct usb_mon_operations {
    void (*urb_submit)(struct usb_bus *bus, struct urb *urb);
    void (*urb_submit_error)(struct usb_bus *bus, struct urb *urb, int err);
    void (*urb_complete)(struct usb_bus *bus, struct urb *urb, int status);
    /* (*urb_unlink)(struct usb_bus *bus, struct urb *urb); */
}
```

Figure 18.4 the initialization action sequence of the usbmon module. During the initialization process, the usbmon registers two types of interface operations with the usbcore module. The first step during initialization operation is to register URB hook operations, and the next step is to register with the usbcore to get device notification on any addition of the new USB bus. While the former helps in hooking URB data, the latter enables creation of usbmon files in the user space using the debugfs. Once these handlers are registered, the usbmon is ready to parse the URB information, and the user can access URB information through the usbmon infrastructure.

The usbcore’s drivers/usb/core/hcd.c provides wrapper functions, namely usbmon_urb_submit, usbmon_urb_complete, and usbmon_urb_submit_error, which subsequently invoke the registered handlers to pass on the URB information. Figure 18.5 illustrates a sequence of function invocations that occur during URB submission and the location you can hook the URB information. The functional driver prepares the URB and it to the

![](bbox=[0.074, 0.683, 0.893, 0.833])

**Figure 18.4**
Initialization sequence of usbmon.