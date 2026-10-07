![](bbox=[0.08, 0.059, 0.65, 0.375])

**Figure 10.1**nA simple breakdown of the Linux USB HCD.

specifications such as the Enhanced Host Controller Interface (EHCI), Universal Host Controller Interface (UHCI), and Open Host Controller Interface (OHCI). Elaborating on these specifications and its Linux implementation is beyond the scope of this book. You are encouraged to explore the implementation on your own at drivers/usb/host/ehci-hcd.c, drivers/usb/host/uhci-hcd.c, or drivers/usb/ohci-hcd.c.

Now that you've seen the functionalities of the HCD, the following section explores the sequence of activities when the host controller is loaded and a USB transfer occurs. Figure 10.2 illustrates the sequence of activities when an HCD loads.

After successful registration of the platform driver, the probe callback of the platform driver creates the HCD object, initializes it, and starts it. If the invocation is successful, the HCD is ready for communication.

Figure 10.3 illustrates a sequence of activities that occurs when a USB transaction starts from the class driver of the Linux USB host framework.

The transfer starts from the class driver with the submission of a URB with a callback to obtain the result of the URB submission. The class driver uses