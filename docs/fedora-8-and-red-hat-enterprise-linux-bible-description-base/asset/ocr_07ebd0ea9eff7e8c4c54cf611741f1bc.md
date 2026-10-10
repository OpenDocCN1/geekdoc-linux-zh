• Device section — Identifies your video card and, optionally, video RAM and clock information for the chipset.

• Screen section — Binds the graphics board and monitor information to be referenced later by the ServerLayout section.

• Keyboard section — Sets keyboard settings, including the layout of the keyboard and the way certain key sequences are mapped to the keyboard.

• Pointer section — Selects the pointer you are using (typically a mouse linked to /dev/mouse). Also sets speed and button emulation, when appropriate.

• DRI — Provides information for Direct Rendering Infrastructure (used for accelerated 3D graphics).

# Configuring video cards for gaming

Some games and video players require special features to work properly (or at all, in some cases). For games that require 3D hardware acceleration, including some that run under TransGaming’s WineX, TransGaming recommends using NVIDIA GeForce Graphics cards.

Because only basic NVIDIA video card drivers are included in Fedora (NVIDIA’s own drivers are not open source), you need to get NVIDIA drivers yourself to use those cards for gaming. You can get Linux NVIDIA drivers from www.nvidia.com/object/linux.html or you can install them from the rpm.livna.org Fedora repository.

> **CAUTION:** Some components of the video drivers from NVIDIA can conflict with those that come with Fedora or RHEL. See the section on choosing a video card for gaming in Chapter 7 for further information on getting and using NVIDIA drivers in Fedora.Games that don’t require 3D hardware acceleration should work fine with most video cards that are supported by the X.Org X server drivers.

> **TIP:** To use hardware DRI acceleration on Voodoo 3 cards, you must have your display set to use 16bpp resolution. On Voodoo 5 cards, only 16bpp and 24bpp resolutions are supported. Voodoo chipssets and other 3DFX technology is now owned by NVIDIA.

# Getting more information

If you tried configuring X and you still have a server that crashes or has a garbled display, your video card may either be unsupported or may require special configuration. Here are several locations you can check for further information:

+   • X.Org (www.x.org) — The latest information about the X servers that come with Fedora and RHEL is available from the X.Org Web site. X.Org is the freeware version of X recently used by many major Linux distributions to replace the XFree86 X server.
+   
+   • X documentation — README files that are specific to different types of video cards are delivered with the X.Org X server. Visit the X doc directory