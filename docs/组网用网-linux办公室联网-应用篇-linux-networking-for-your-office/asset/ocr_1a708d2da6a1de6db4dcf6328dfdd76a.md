(http://www.suse.com) develops many of the cutting-edge XFree86 drivers, so you might find an experimental driver there for a relatively new video board. If you find that you're in possession of an extremely new and unsupported board, it's possible that the Xi Graphics (http://www.xig.com) Accelerated X server supports your board; but purchasing this software might be more expensive than buying a replacement video card.

Video boards, like many computer components, have their own memory. This memory is used to hold the contents of the screen, and sometimes to help with 3D rendering or other features. As you increase the resolution and color depth of your display, you increase the amount of memory required on the video board. You can compute the amount required to run the board at any given resolution with the following formula:

M = x × y × d / 8,388,608

In this equation, M is the memory in megabytes, x and y are the x and y resolutions, and d is the color depth (for instance, 16 for 16-bit color, capable of displaying 65,536 colors). Most video cards on the market today have more than enough RAM to handle a display of 1024×768 or even 1600×1200 at 16-bit, and often at 24-bit or 32-bit. Keep in mind that the speed of the display drops as the screen resolution, and especially the color depth, increases.

# Sound Cards

In general, you don't need a sound card for a server. If you want one nonetheless, you should know that there are three major sources of drivers for sound cards in Linux:

+   - The Linux kernel—The kernel includes a set of drivers for a number of sound cards. Many of these are older ISA designs, but some are newer PCI cards.

+   - The OSS drivers—4Front Technologies (http://www.4front.com/) offers the commercial Open Sound System (OSS) drivers for Linux. These drivers are related to the drivers in the Linux kernel, but are available only for a fee.

+   - The ALSA drivers—The Advanced Linux Sound Architecture (ALSA; http://alsa.jcu.cz/) project is working on a new sound model for Linux, and has a set of drivers available.

Linux sound driver development and the sound card marketplace both change rapidly, so it's difficult to make definite recommendations. ISA boards based on assorted Crystal Semiconductor chipsets are well supported, however, under all three driver sets, and PCI boards based on the S3 SonicVibes chipset are also popular.