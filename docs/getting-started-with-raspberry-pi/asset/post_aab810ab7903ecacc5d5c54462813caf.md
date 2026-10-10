
| Kernel Interface | Location | Description |
| :--- | :--- | :--- |
| usb_register() | include/linux/usb.h | Registers a usb_driver with the USB core |
| usb_deregister() | drivers/usb/core/driver.c | Unregisters a usb_driver from the USB core |
| usb_set_intdata() | include/linux/usb.h | Attaches device-specific data to a usb_interface |
| usb_get_intdata() | include/linux/usb.h | Detaches device-specific data from a usb_interface |
| usb_register_dev() | drivers/usb/core/file.c | Associates a character interface with a USB client driver |
| usb_deregister_dev() | drivers/usb/core/file.c | Dissociates a character interface from a USB client driver |
| usb_alloc_urb() | drivers/usb/core/urb.c | Allocates a URB |
| usb_fill_[control\|int\|bulk]_urb() | include/linux/usb.h | Populates a URB |
| usb_[control\|interrupt\|bulk]_msg() | drivers/usb/core/message.c | Wrappers for synchronous URB submission |
| usb_submit_urb() | drivers/usb/core/urb.c | Submits a URB to the USB core |
| usb_free_urb() | drivers/usb/core/urb.c | Frees references to a completed URB |
| usb_unlink_urb() | drivers/usb/core/urb.c | Frees references to a pending URB |
| usb_[rcv\|snd]_[ctrl\|int\|bulk\|isoc]pipe() | include/linux/usb.h | Creates a USB pipe |
| usb_find_interface() | drivers/usb/core/usb.c | Gets the usb_interface associated with a USB client driver |
| usb_buffer_alloc() | drivers/usb/core/usb.c | Allocates a consistent DMA transfer buffer |
| usb_buffer_free() | drivers/usb/core/usb.c | Frees a buffer that was allocated using usb_buffer_alloc() |
| usb_serial_register() | drivers/usb/serial/usb-serial.c | Registers a driver with the USB-Serial core |
| usb_serial_deregister() | drivers/usb/serial/usb-serial.c | Unregisters a driver from the USB-Serial core |
| usb_gadget_register_driver() | Device controller drivers in drivers/usb/gadget/ | Registers a gadget with a device controller driver |

## Chapter 12. Video Drivers

### In This Chapter

- 356 Display Architecture
- 359 Linux-Video Subsystem
- 361 Display Parameters
- 362 The Frame Buffer API
- 365 Frame Buffer Drivers
- 380 Console Drivers
- 387 Debugging
- 388 Looking at the Sources

Video hardware generates visual output for a computer system to display. In this chapter, let's find out how the kernel supports video controllers and discover the advantages offered by the frame buffer abstraction. Let's also learn to write console drivers that display messages emitted by the kernel.

## Display Architecture

Figure 12.1 shows the display assembly on a PC-compatible system. The graphics controller that is part of the North Bridge (see the sidebar "The North Bridge") connects to different types of display devices using several interface standards (see the sidebar "Video Cabling Standards").

### Figure 12.1. Display connection on a PC system.

![](img/07cc6f9c8c74622020874f66bfb53dc4_330_0.png)

Video Graphics Array (VGA) is the original display standard introduced by IBM, but it's more of a resolution specification today. VGA refers to a resolution of 640x480, whereas newer standards such as eXtended Graphics Array (XGA) and Super Video Graphics Array (SVGA) support higher resolutions of 800x600 and 1024x768. Quarter VGA (QVGA) panels having a resolution of 320x240 are common on embedded devices, such as handhelds and smart phones.

Graphics controllers in the x86 world compatible with VGA and its derivatives offer a character-based text mode and a pixel-based graphics mode. The non-x86 embedded space is non-VGA, however, and has no concept of a dedicated text mode.

## The North Bridge

In earlier chapters, you learned about peripheral buses such as LPC, I²C, PCMCIA, PCI, and USB, all of which are sourced from the South Bridge on PC-centric systems. Display architecture, however, takes us inside the North Bridge. A North Bridge in the Intel-based PC architecture is either a Graphics and Memory Controller Hub (GMCH) or a Memory Controller Hub (MCH). The former contains a memory controller, a Front Side Bus (FSB) controller, and a graphics controller. The latter lacks an integrated graphics controller but provides an Accelerated Graphics Port (AGP) channel to connect external graphics hardware.

Consider, for example, the Intel 855 GMCH North Bridge chipset. The FSB controller in the 855 GMCH interfaces with Pentium M processors. The memory controller supports Dual Data Rate (DDR) SDRAM memory chips. The integrated graphics controller lets you connect to display devices using analog VGA, LVDS, or DVI (see the sidebar "Video Cabling Standards"). The 855 GMCH enables you to simultaneously send output to two displays, so you can, for example, dispatch similar or separate information to your laptop's LCD panel and an external CRT monitor at the same time.

Recent North Bridge chipsets, such as the AMD 690G, include support for HDMI (see the following sidebar) in addition to VGA and DVI.

Several interfacing standards specify the connection between video controllers and display devices. Display devices and the cabling technologies they use follow:

- An analog display such as a *cathode ray tube* (CRT) monitor that has a standard VGA connector.
- A digital flat-panel display such as a laptop *Thin Film Transistor* (TFT) LCD that has a *low-voltage differential signaling* (LVDS) connector.
- A display monitor that complies with the *Digital Visual Interface* (DVI) specification. DVI is a standard developed by the *Digital Display Working Group* (DDWG) for carrying high-quality video. There are three DVI subclasses: *digital-only* (DVI-D), *analog-only* (DVI-A), and *digital-and-analog* (DVI-I).
- A display monitor that complies with the *High-Definition Television* (HDTV) specification using the *High-Definition Multimedia Interface* (HDMI). HDMI is a modern digital audio-video cable standard that supports high data rates. Unlike video-only standards such as DVI, HDMI can carry both picture and sound.

Embedded SoCs usually have an on-chip LCD controller, as shown in Figure 12.2. The output emanating from the LCD controller are TTL (*Transistor-Transistor Logic*) signals that pack 18 bits of flat-panel video data, six each for the three primary colors, red, green, and blue. Several handhelds and phones use QVGA-type internal LCD panels that directly receive the TTL flat-panel video data sourced by LCD controllers.

### Figure 12.2. Display connection on an embedded system.

![](img/07cc6f9c8c74622020874f66bfb53dc4_331_0.png)

The embedded device, as in Figure 12.3, supports dual display panels: an internal LVDS flat-panel LCD and an external DVI monitor. The internal TFT LCD takes an LVDS connector as input, so an LVDS transmitter chip is used to convert the flat-panel signals to LVDS. An example of an LVDS transmitter chip is DS90C363B from National Semiconductor. The external DVI monitor takes only a DVI connector, so a DVI transmitter is used to convert the 18-bit video signals to DVI-D. An I²C interface is provided so that the device driver can configure the DVI transmitter registers. An example of a DVI transmitter chip is SiI164 from Silicon Image.

![](img/07cc6f9c8c74622020874f66bfb53dc4_332_0.png)

![](img/07cc6f9c8c74622020874f66bfb53dc4_332_1.png)

## Linux-Video Subsystem

The concept of frame buffers is central to video on Linux, so let's first find out what that offers.

Because video adapters can be based on different hardware architectures, the implementation of higher kernel layers and applications might need to vary across video cards. This results in nonuniform schemes to handle different video cards. The ensuing nonportability and extra code necessitate greater investment and maintenance. The frame buffer concept solves this problem by describing a general abstraction and specifying a programming interface that allows applications and higher kernel layers to be written in a platform-independent manner. Figure 12.4 shows you the frame buffer advantage.

![](img/07cc6f9c8c74622020874f66bfb53dc4_333_0.png)

The kernel's frame buffer interface thus allows applications to be independent of the vagaries of the underlying graphics hardware. Applications run unchanged over diverse types of video hardware if they and the display drivers conform to the frame buffer interface. As you will soon find out, the common frame buffer programming interface also brings hardware independence to kernel layers, such as the frame buffer console driver.

Today, several applications, such as web browsers and movie players, work directly over the frame buffer interface. Such applications can do graphics without help from a windowing system.

The X Windows server (Xfvdev) is capable of working over the frame buffer interface, as shown in Figure 12.5.
