The following illustrates a Device section, which must begin with an Identifier entry:

```
```
Section "Device"
    Identifier "MagicGraph NM2160"
    VendorName "Unknown"
    BoardName "Unknown"
    VideoRam 2048
    Chipset "NM2160"
    IOBase 0xfea00000
    MemBase 0xfd000000
    DacSpeed 90
    Option "intern_disp"
EndSection
```
```

# DEVICES SECTION ENTRIES

| Use This Entry | To Do This |
| :--- | :--- |
| BIOSBase *address* | Specify the base address of the video BIOS if it is other than the default of 0xC0000. |
| BoardName *name* | Specify the name of the graphics adapter. For a list of supported graphics devices, see /usr/lib/X11/Cards in the X11 directory. |
| Chipset *chipset* | Specify the chipset used by the graphics adapter if this is not determined by the server’s probe. |
| COPBase *address* | Specify the base address of the coprocessor, which is needed for some servers. Consult the server’s documentation. |
| DACBase *address* | Specify the base address of the DAC, which is needed for some servers. Consult the server’s documentation. |
| Instance *n* | Indicate whether the video circuitry is indicated on the motherboard, which is needed for some servers. Consult the server’s documentation. |
| IOBase *address* | Specify the base address of the video I/O, which is needed for some servers. Consult the server’s documentation. |