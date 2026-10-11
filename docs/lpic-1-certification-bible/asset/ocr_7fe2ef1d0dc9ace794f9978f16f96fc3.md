|  |  |
| --- | --- |
| ScrollLock | Compose |
| RightCtl | Control |
| XkbKeycodes | "xfree86" |
| XkbTypes | "default" |
| XkbCompat | "default" |
| XkbSymbols | "us(pc101)" |
| XkbGeometry | "pc" |
| XkbRules | "xfree86" |
| XkbModel | "pc101" |
| XkbLayout | "us" |
| EndSection |  |

# Pointer

This section configures the pointing device. If this is not configured correctly, the X server may not start, or the mouse may act erratically. Table 9-3 shows the available configuration entries for this section. The following is an example:

```
# ************************************************
# Pointer section
# ************************************************

Section "Pointer"
    Protocol    "IMPS/2"
    Device      "/dev/mouse"
    ZAxisMapping 4 5
EndSection
```

| Table 9-3 Pointer Section Entries |
| Entry | Function |
| Protocol "Protocol Name" | Specifies the protocol that the mouse device uses. Check the XF86Config man page for the complete list of available protocols. |
| Device "Device Path" | Specifies the device to use to communicate with the mouse. For example, /dev/mouse. |
| Port "Device Path" | This is an alternative to the Device entry. |
| BaudRate <baud rate> | Sets the baud rate for a serial mouse. |
| Buttons N | Specifies the pointing device has N number of buttons. |
| Emulate3Buttons | Allows a two-button mouse to emulate a three-button mouse by registering the third button when both buttons are pressed. |