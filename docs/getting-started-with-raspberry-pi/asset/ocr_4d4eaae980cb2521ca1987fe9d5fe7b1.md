The navigation system's video software is broadly architected as a GPS application operating over a low-level frame buffer driver for the LCD controller. The application fetches location coordinates from the GPS receiver by reading `/dev/ttySX`, where *X* is the UART number connected to the receiver. It then translates the geographic fix information into a picture and writes the pixel data to the frame buffer associated with the LCD controller. This is done on the lines of Listing 12.1, except that picture data is dispatched rather than zeros to clear the screen.

The rest of this section focuses only on the low-level frame buffer device driver. Like many other driver subsystems, the full complement of facilities, modes, and options offered by the frame buffer core layer are complex and can be learned only with coding experience. The frame buffer driver for the example navigation system is relatively simplistic and is only a starting point for deeper explorations.

Table 12.1 describes the register model of the LCD controller shown in Figure 12.6. The frame buffer driver in Listing 12.2 operates over these registers.

**Table 12.1. Register Layout of the LCD Controller Shown in Figure 12.6**

| Register Name | Used to Configure |
|---|---|
| SIZE_REG | LCD panel's maximum X and Y dimensions |
| HSYNC_REG | HSYNC duration |
| VSYNC_REG | VSYNC duration |
| CONF_REG | Bits per pixel, pixel polarity, clock dividers for generating pixelclock, color/monochrome mode, and so on |
| CTRL_REG | Enable/disable LCD controller, clocks, and DMA |
| DMA_REG | Frame buffer's DMA start address, burst length, and watermark sizes |
| STATUS_REG | Status values |
| CONTRAST_REG | Contrast level |

Our frame buffer driver (called *myfb*) is implemented as a platform driver in Listing 12.2. As you learned in Chapter 6, a platform is a pseudo bus usually used to connect lightweight devices integrated into SoCs, with the kernel's device model. Architecture-specific setup code (in *arch/your-arch/platform/*) adds the platform using `platform_device_add()`; but for simplicity, the `probe()` method of the *myfb* driver performs this before registering itself as a platform driver. Refer back to the section “Device Example: Cell Phone” in Chapter 6 for the general architecture of a platform driver and associated entry points.

# ### Data Structures

Let's take a look at the major data structures and methods associated with frame buffer drivers and then zoom in on *myfb*. The following two are the main structures:

+   1. `struct fb_info` is the centerpiece data structure of frame buffer drivers. This structure is defined in `include/linux/fb.h` as follows:
+   
+      ```
+      struct fb_info {
+      /* ... */
+      struct fb_var_screeninfo var; /* Variable screen information. */