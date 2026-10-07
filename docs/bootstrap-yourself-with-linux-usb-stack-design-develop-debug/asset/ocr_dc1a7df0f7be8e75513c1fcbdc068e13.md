# Overview of usbfs 29

following section extracts a portion of proc_devices.txt. In the example setup, a thumb drive is connected to bus number 07. Will you now dissect the contents specific to the thumb drive from the devices file.

The first line of the text information starts with the keyword T. The text in this line indicates that the thumb drive is a high-speed device with device address 3. From the line, you can also understand that the device is connected to port 02 of bus number 07. All this information is in decimal format.

```
T: Bus=07 Lev=01 Prnt=01 Port=02 Cnt=01 Dev#=3 Spd=480 MxCh=0
```

The second line starts with the keyword D indicates that the line contains device descriptor information. The line indicates that the thumb drive is a USB 2.0 device with one configuration.

```
D: Ver=2.00 Cls=00(1) Sub=00 Prot=00 MxPS=64 #Cfgs=1]
```

The subsequent line starts with the keyword P contains product-specific information. The line provides the product and the vendor ID of the thumb drive.

```
P: Vendor=1221 ProID=3234 Rev=00
```

The line that starts with the keyword S provides information as a string. This includes the manufacturer name, the product name, and the serial number of the device.

+   S: Manufacturer=Udisk
S: Product=Udisk 2.0
S: SerialNumber=013CCCFFFAE59D

The next line starts with the keyword C indicates device configuration-related information. The line indicates the thumb drive. The * indicates that the current configuration is the active one.

```
C*: #Ifs=1 Cfg#=1 Atr=80 MxPwr=10=0mA
```

The line that starts with the keyword I indicates interface-related information. The devices interface two endpoints and a storage device. Because it is a storage device, the usb-storage module is loaded as the driver for the interface.

```
I*: If#=0 Alt=0 #EPs=2 Cls=08(stor.) Sub=06 Prot=50 Driver=usb-storage
```

The line that starts with the keyword E indicates endpoint-related information. Because it is a thumb drive, it has bulk IN and bulk OUT endpoints with a max