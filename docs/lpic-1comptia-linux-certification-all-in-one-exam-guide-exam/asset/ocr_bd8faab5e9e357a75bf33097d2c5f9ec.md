When working with I/O addresses, there are a number of important facts to keep in mind:

+   - All devices must have an I/O address assigned.
+   - Most devices will use a range of I/O addresses.
+   - Devices must use unique I/O ports.
+   - Default I/O port assignments:
+     - 0000h – DMA Controller
+     - 0020h – PIC 1
+     - 0030h – PIC 2
+     - 0040h – System Timer
+     - 0060h – Keyboard
+     - 0070h – CMOS Clock
+     - 00C0h – DMA Controller
+     - 00F0h – Math Co-processor
+     - 0170h – Secondary IDE Hard Disk Controller
+     - 01F0h – Primary IDE Hard Disk Controller
+     - 0200h – Joystick
+     - 0278h – LPT2
+     - 02E8h – COM4
+     - 02F8h – COM2
+     - 0378h – LPT1
+     - 03E8h – COM3
+     - 03F0h – Floppy Disk Drive Controller
+     - 03F8h – COM1

# Direct Memory Access Channels

In addition to interrupts and I/O addresses, some devices also require that you configure them with a direct memory access (DMA) channel. DMA channels are used by high-throughput devices to communicate directly with RAM without involving the CPU. By-passing the CPU can dramatically increase the device’s data transfer rate.

Not all devices need DMA. Other device, however, would be severely handicapped if they couldn’t use DMA. These devices include

+   - Sound boards
+   - Floppy diskette drives
+   - Some hard disk drives

DMA is implemented on the motherboard using the DMA controller chip (DCC). The DCC is very similar to the PIC chip we reviewed earlier. The DCC has four leads