driver framework. When the function is successful, it returns 0; when it
fails, it returns a negative value.

+   - void usb_composite_unregister(struct usb_composite_driver *);

This function acts as an interface to unregister class drivers using the
composite driver framework. This is a wrapper above the gadget interface
istration function usb_gadget_unregister_driver by the composite
driver framework. When the function is successful, it returns 0; when it
fails, it returns a negative value.

+   - int usb_add_function(struct usb_configuration *, struct usb_function *);

This method adds a function to a configuration and calls the bind
method to allocate resources such as interface IDs and endpoints. It runs
in a single-threaded context. When the function is successful, it returns
0; when it fails, it returns a negative value.

+   - int usb_add_config(struct usb_composite_dev *, struct usb_configura-tion *)

This method adds a configuration to a device and binds the configura-
tions global resources, including string IDs and per-configuration
resources such as interface IDs and endpoints. It runs in a single-
ted context. When the function is successful, it returns 0; when it
fails, it returns a negative value.

Now you've seen the important data structure of the functional drivers, the
subsequent section details the internal activity of the composite framework and
the functional driver.

# CLASS DRIVER: DESIGN

The functional driver layer sits on top of the gadget driver layer implementing
actual USB device functionality. The functional driver is also referred to as the
class driver. The USB group defines the USB device functionality through USB
class specifications. Like other layers of the gadget subsystem, the functional
driver source is available in drivers/usb/gadget/, and the source files are named
based on the class or function they support.