+   * A PnP-compatible device
+   * A PnP-compatible operating system

When the system is powered on, the PnP BIOS negotiates with the PnP expansion board to determine what interrupt, I/O addresses, and DMA channels it will use. If necessary, the operating system can also add its input as to what resources it thinks should be assigned.

> **NOTE** In the earliest version of PnP, the system didn’t always operate correctly. System administrators called it “plug-n-pray.”

PnP is used for all modern expansion boards. In the late 1990s, there were even some 16-bit ISA motherboards and cards that also supported PnP.

Next, let’s look at managing integrated PC devices.

# # Managing Integrated Devices

In the old days, the typical PC motherboard was pretty much bare bones in its design. Basically, you had the CPU socket, your chipset components, your expansion slots, and not much else. If you wanted to connect serial or parallel devices to the board, you had to install the appropriate board in an expansion slot. If you wanted to actually see your video output, you likewise had to install a video board in an expansion slot. To connect the system to a network, you had to (you guessed it) install a network interface in an expansion slot. Oh, and by the way, if you wanted to use any kind of floppy or hard disk, you also had to install a disk controller board in an expansion slot. Don’t even get me started on getting a sound board to work in these old systems.

Today, things are much different. Most motherboards include a plethora of integrated devices on board, including

+   * I/O ports (including serial, parallel, USB, and FireWire)
+   * Video interfaces
+   * Network interfaces
+   * Sound boards
+   * Storage controllers
+   * And so on...

Integrated peripherals are nice. They reduce the overall cost of building the system because you don’t have to buy all of these devices separately. They make it easier to manage as well because the components (usually) all play nicely together and all of the drivers needed to support the devices are included with the board.

However, suppose the video, network, or sound interface integrated into the motherboard in your system aren’t up to snuff in your reckoning? Maybe you’re a gamer and