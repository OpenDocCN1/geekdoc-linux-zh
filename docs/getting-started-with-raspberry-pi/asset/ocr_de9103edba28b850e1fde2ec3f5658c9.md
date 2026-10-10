```
```
usb_deregister(&tele_driver);
return;
}

module_init(usb_tele_init);
module_exit(usb_tele_exit);
```
```

The `USB_DEVICE()` macro creates a `usb_device_id` from the vendor and product IDs supplied to it. This is analogous to the `PCI_DEVICE()` macro discussed in the previous chapter. The `MODULE_DEVICE_TABLE()` macro marks `tele_ids` in the module image so that the module can be loaded on demand if the card is hotplugged. This is again similar to what we discussed for PCMCIA and PCI devices in the previous two chapters.

When the USB core detects a device with properties matching the ones declared in the `usb_device_id` table belonging to a client driver, it invokes the `probe()` method registered by that driver. When the device is unplugged or if the module is unloaded, the USB core invokes the driver's `disconnect()` method.

Listing 11.3 implements the `probe()` and `disconnect()` methods of the telemetry driver. It starts by defining a device-specific structure, `tele_device_t`, which contains the following fields:

+   - A pointer to the associated `usb_device`.

+   - A pointer to the `usb_interface`. Revisit Listing 11.1 to see this structure in use.

+   - A control URB (`ctrl_urb`) to communicate with the telemetry configuration register, and a `ctrl_req` to formulate programming requests to this register. These fields are described in the next section "Accessing Registers."

+   - The card has a bulk IN endpoint through which you can glean the collected telemetry information. Associated with this endpoint are three fields: `bulk_in_addr`, which holds the endpoint address; `bulk_in_buf`, which stores received data; and `bulk_in_len`, which contains the size of the receive data buffer.

+   - The card has a bulk OUT endpoint to facilitate downstream data transfer. `tele_device_t` has a field called `bulk_out_addr` to store the address of this endpoint. There are fewer data structures in the OUT direction because in this simple case we use a synchronous URB submission interface that hides several implementation details.

Khudd invokes the card's `probe()` method, `tele_probe()`, soon after enumeration. `tele_probe()` performs three tasks: