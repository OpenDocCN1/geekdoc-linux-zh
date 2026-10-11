USB ports also require interrupts, but the interrupt assigned to USB ports varies substantially from one machine to another. Because most USB ports are PCI devices that are built in to the motherboard, it's usually not necessary to explicitly configure a USB port's interrupt.

# ## I/O Ports

The term I/O port can be confusing, because it can refer either to an interface into which you can plug a device or to a small area of memory used by the x86 architecture to transfer data between the CPU and its devices. Serial and parallel ports, like other hardware, require access to certain I/O port ranges, as detailed in Table 16.1.

Like shared interrupts, shared I/O ports on serial ports can be a problem. You should be sure to change the I/O ports for such serial devices in much the same way as you change their interrupts—either disable a built-in device and let the add-on device take over the built-in device's settings, or assign an unused I/O port to the device. You can find a list of used I/O ports in Linux by typing cat /proc/ioports. This command produces output similar to the following:

```
```
0000-001f : dma1
0020-003f : pic1
0040-005f : timer
0060-006f : keyboard
0080-008f : dma page reg
00a0-00bf : pic2
00c0-00df : dma2
00f0-00ff : fpu
02f8-02ff : serial(auto)
0378-037a : parport0
03c0-03df : vga+
03f8-03ff : serial(auto)
0778-077a : parport0
da00-da ff : eth0
```
```

You can use this list to select an appropriate free I/O port range. Be aware, however, that if a device hasn't been used recently, its assigned I/O ports might not appear in this list. You should therefore check the /proc/ioports file shortly after using every device you have on the computer.

# ### Cabling Concerns

Except for internal modems, serial and parallel devices require cables. Figure 16.1 shows several types of serial and parallel cable connectors for reference. With the exception of the USB Series B and Centronics parallel port connectors, all these connectors plug into ports on the back of x86 computers. The USB Series B and Centronics parallel port connectors both connect to devices, such as printers, that interface via the USB and parallel ports, respectively.