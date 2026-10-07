```
/* extra dual-role default-b states */
OTG_STATE_B_WAIT_ACON,
OTG_STATE_B_HOST,
/* dual-role default-a */
OTG_STATE_A_IDLE,
OTG_STATE_A_WAIT_VRISE,
OTG_STATE_A_WAIT_BCON,
OTG_STATE_A_HOST,
OTG_STATE_A_SUSPEND,
OTG_STATE_A_PERIPHERAL,
OTG_STATE_A_WAIT_VFALL,
OTG_STATE_A_VBUS_ERR;
```

:

The next section explores how the Linux USB subsystem uses these OTG interfaces to enable the USB host framework to a USB gadget in an OTG setup or vice versa.

# OTG DRIVER FRAMEWORK

The OTG framework is not clearly defined like the gadget framework is; sometimes the OTG implementation is mixed with the other frameworks. The Linux USB subsystem source code of the OTG framework is maintained in the /drivers/usb/otg/ folder. Some part of the usbcore module plays a key role (drivers/usb/core/hub.c).

Most of the OTG activities are based on the physical layer activity and the timing of the electrical signals. The role of the OTG software framework is minimal; it is responsible for setting up the signal and switching to different states defined by the OTG specification. Figure 15.2 illustrates a top-level breakdown of the OTG framework.

The OTG framework is divided into two major parts: callback methods and utility functions. The methods provided by struct otg_transceiver are extended to the other Linux USB frameworks using wrapper functions. The OTG framework also helps save and retrieve the struct otg_transceiver object using utility functions. The other main part is interface methods of the transceiver to the platform.