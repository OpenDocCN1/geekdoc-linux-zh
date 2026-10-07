}
--cut-
--cut--

```
dev->udev = usb_get_interface_usb_dev(interface_to_usbdev(interface));
dev->interface = interface;
```

```
iface_desc = interface->cur_altsetting;
for (i = 0; i < iface_desc->desc.bNumEndpoints; ++i) {
    endpoint = &iface_desc->endpoint[i].desc;
```

--cut-
usb_set_intfdata(interface, dev);

```
/* we can register the device now, as it is ready */
retval = usb_register_dev(interface, &skel_class);
```

--cut-
--cut-
}

A successful registration allows the driver to take control of the interface and start communicating with the device.

When the device is disconnected or becomes unbound, the disconnect callback method is invoked. The disconnect callback should release the acquired resources and return the interface taken earlier. After successful release of resources, the driver should be deregistered from the usbcore using the interface functions.

```
static void skel_disconnect(struct usb_interface *interface) {
--cut-
--cut-
--cut-
dev = usb_get_intfdata(interface);
usb_set_intfdata(interface, NULL);
```

```
/* give back our minor * */
usb_deregister_dev(interface, &skel_class);
--cut-
--cut-
}
```