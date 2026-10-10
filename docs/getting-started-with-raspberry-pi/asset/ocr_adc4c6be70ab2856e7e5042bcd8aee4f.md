```
```
D:  Ver= 1,10 Cls=09(hub ) Sub=00 Prot=00 MxPS=64 #Cfgs=   1
...
T:  Bus=05 Lev=01 Prnt=01 Port=00 Cnt=01 Dev#=  3 Spd=12  MxCh= 0
D:  Ver= 1.01 Cls=00(>IFC) Sub=00 Prot=00 MxPS=16 #Cfgs=   1
P:  Vendor=12d1 ProdID=1001 Rev= 0.00
S:  Manufacturer=Huawei Technologies
S:  Product=Huawei Mobile
C:* #Ifs= 2 Cfg#= 1 Atr=e0 MxPwr=100mA
I:  If#= 0 Alt= 0 #EPs= 3 Cls=ff(vend.) Sub=ff Prot=ff Driver=p12303
E:  Ad=81(I)  Atr=03(Int.) MxPS=   16 Ivl=128ms
E:  Ad=8a(I)  Atr=02(Bulk) MxPS=   64 Ivl=0ms
E:  Ad=0b(O)  Atr=02(Bulk) MxPS=   64 Ivl=0ms
I:  If#= 1 Alt= 0 #EPs= 2 Cls=ff(vend.) Sub=ff Prot=ff Driver=p12303
E:  Ad=83(I)  Atr=02(Bulk) MxPS=   64 Ivl=0ms
E:  Ad=06(O)  Atr=02(Bulk) MxPS=   64 Ivl=0ms
...
```
```

The top three entries (*bus7*, *bus6*, and *bus5*) correspond to the three host controllers present in the CDMA card. The last entry shows that a full-speed (12Mbps) USB device is connected to bus 5. This device has a vendorID of 0x12d1 and a productID of 0x1001. As is evident from the preceding output, the USB core has bound this device to the p12303 driver. If you look at the source file of the PL2303 Prolific USB-to-serial adapter driver (*drivers/usb/serial/pl2303.c*), you will find the following member in the usb_device_id table:

```
```
static struct usb_device_id id_table [] = {
/* ... */
 {USB_DEVICE(HUAWEI_VENDOR_ID, HUAWEI_PRODUCT_ID)},
/* ... */
};
```
```

A quick peek at p12303.h living in the same directory confirms that HUAWEI_VENDOR_ID and HUAWEI_PRODUCT_ID match the values that you just gleaned from */proc/bus/usb/devices*. The p12303 driver presents a serial interface, */dev/ttyUSB0*, over the detected USB-to-serial converter. You can send *AT* commands to the CDMA modem over this interface. Attach *pppd* over this device and connect to the net. You are now a 3G surfer!