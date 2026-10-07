# Chapter 18 = Debugging Using Linux USB

cad4aa80 2613121452 S Ci:7:005:0 s 80 06 0200 0000 09 9 <ncad4aa80 2613121662 Ci:7:005:0 9 = 0922050 01010080 32

The log format matches the struct usb_mon_event data structure discussed in the previous section. The following section dissects the usbmon log in a more detailed manner.

Notice that the log starts with a URB address (d2263a80) followed by the URB submission time (2613100221). The time stamp along with the USB-related information helps in measuring the time taken to complete a URB transaction. Figure 18.7 provides a detailed breakdown of the usbmon log.

This section dissects a sample from mass storage driver's URB transfer. The following terminal activity is a capture of command block wrapper (CBW) transfers from storage device 5 and bulk endpoint number 1. Figure 18.8 provide a detailed breakdown of the usbmon storage log.

d2263780 2618I25421 S Bo:7:005:1 -115 31 = 55534243 01000000 24000000 80000612
0000024 00000000 000000000

| URB Address | Time Stamp | Transfer & Event | Bus Number | Device Number | Endpoint Number | URB Status | Type | bRequest | wValue | wIndex |
|---|---|---|---|---|---|---|---|---|---|---||
| d2263a80 | 2613100221 | | Co | | | | s | | 5 | 0 |

| URB Address | Time Stamp | Transfer & Event | Bus Number | Device Number | Endpoint Number | URB Status | Type | bRequest | wValue | wIndex | wLength (Hex) | wLength (Decimal) | Direction (IN) |
|---|---|---|---|---|---|---|---|---|---|---|---|---||
| d2263a80 | 2613112192 | | | | | | s | 80 | 0 | 100 | 7c | 12 | < |

| URB Address | Time Stamp | Transfer & Event | Bus Number | Device Number | Endpoint Number | URB Status | Length | bLength&Descriptor/Type bUSB | DeviceSubClass&Protocol MaxSize (HEX) | Vendor ID (Product) | iManufacturer Product | iSerialNumber&Configuration |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---||
| d2263a80 | 2613121399 | | Ci | | | 5 | | 18 | 12010052 | 0000040 | 2112342 | 0006102 | 0301 |

Figure 18.7
The usbmon command data.

| URB Address | Time Stamp | Transfer & Event | Bus Number | Device Number | Endpoint Number | URB Status | Length | Mass Storage Information |
|---|---|---|---|---|---|---|---|---||
| d2263780 | 2618I25421 | | Bo | 7 | 5 | | -115 | 31 | 55534243 01000000 80000612 24000000 000000000 000000000 |

Figure 18.8
The usbmon bulk data.