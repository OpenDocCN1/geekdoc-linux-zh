# Chapter 15 = Linux USB OTG Driver

This callback method receives the USB host data structure and saves it in the transceiver driver for subsequent usage. The interface function int otg_set_host(struct otg_transceiver *otg, struct usb_bus *host) sets this information.

+   - int (*peripheral)(struct otg_transceiver *otg, struct usb_gadget *gadget);

This callback method receives the USB device data structure and saves it in the transceiver driver for subsequent usage. The interface function int otg_set_peripheral(struct otg_transceiver *otg, struct usb_gadget *periph) sets this information.

+   - int (*power)(struct otg_transceiver *otg, unsigned mA);

This callback method sets the power in the VBUS during a default-B session. The interface function int otg_set_power(struct otg_transceiver *otg, unsigned mA) invokes this callback.

+   - int (*suspend)(struct otg_transceiver *otg, int suspend);

This callback method suspends and resumes the transceiver. When the suspend parameter is set, the transceiver is to be suspended; when it is 0, the transceiver is to be resumed. The interface function int otg_set_suspend(struct otg_transceiver *otg, int suspend) invokes this callback.

+   - int (*start_rp)(struct otg_transceiver *otg);

This callback method starts the SRP session, and the transceiver driver or hardware layer implements this callback. The interface function int otg_start_rp(struct otg_transceiver *otg) invokes this callback.

The OTG specification defines the state machine as part of the negotiation protocols, and the Linux USB framework define part of an enum usb_otg_state in include/linux/usb/otg.h.

```
enum usb_otg_state {
    OTG_STATE_UNDEFINED = 0,
    /* single-role peripheral, and dual-role default-b suspend */
    OTG_STATE_B_IDLE,
    OTG_STATE_B_SRP_INIT,
    OTG_STATE_B_PERIPHERAL,
```