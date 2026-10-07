# Bootstrap Essentials: OTG Driver

```
/* to pass extra port status to the root hub */
u16
port_status;
u16
port_change;
/* initialize/shutdown of the OTG controller */
int    (*init)(struct otg_transceiver *otg);
void   (*shutdown)(struct otg_transceiver *otg);
/* bind/unbind the host controller */
int    (*host)(struct otg_transceiver *otg,
        struct usb_bus *host);
/* bind/unbind the peripheral controller */
int    (*peripheral)(struct otg_transceiver *otg,
        struct usb_gadget *gadget);
/* effective for B devices, ignored for A-peripheral */
int    (*set_power)(struct otg_transceiver *otg,
    unsigned mA);
/* effective for A-peripheral, ignored for B devices */
int    (*set_vbus)(struct otg_transceiver *otg,
    bool enabled);
/* for non-OTG B devices: set transceiver into suspend mode */
nint    (*set_suspend)(struct otg_transceiver *otg,
    int suspend);
/* for B devices only: start session with A-Host */
nint    (*start_srp)(struct otg_transceiver *otg);
/* start or continue HNP role switch */
nint    (*start_hnp)(struct otg_transceiver *otg);
```

);

The struct otg_transceiver data structure provides callback methods to implement the framework that is necessary for the OTG callback. These methods help the Linux USB framework manage the OTG requirement.  The following list details the methods of the OTG framework.

+   * int (*start_hnp)(struct otg_transceiver *otg);
This callback method starts the HNP session. The transceiver driver or hardware layer implements this callback. The interface function int otg_start_hnp(struct otg_transceiver *otg) invokes this callback.

+   * int (*set_host)(struct otg_transceiver *otg, struct usb_bus *host);