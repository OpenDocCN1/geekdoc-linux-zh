# Understanding Serial Devices 399

Figure 12.3 USB support requires selecting drivers for specific USB devices.

![](bbox=[0.168, 0.153, 0.802, 0.574])

# Administrator's Logbook: Enabling USB Support

System: E12345678

Action: Patched 2.2.17 kernel with USB support and recompiled, enabling support for USB mice and modems. Installed in LILO as 2217-usb.

characters to this device file. For instance, the following command sends the string ATDT555-4321 to a modem attached to /dev/ttyS0, causing the modem to dial 555-4321.

```
S echo "ATDT555-4321" > /dev/ttyS0
```

Communicating with Devices PART 4