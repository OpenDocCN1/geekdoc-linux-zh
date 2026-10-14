# Graphics Cards / X server

Next, you must specify your graphics card:

*Do you want to look at the card database?*

If you enter ‘y’, a selection of predefined cards is presented. Here, select your card by pressing the corresponding number. Do not trust this list blindly, since there can be differences in clock chip and RAMDAC³ settings.

This is why a menu item appears later for selecting a RAMDAC and a clock chip, even though you have entered them already. Then the predefined settings for this card will be presented as an extra option.

The card definitions contain information on clock chips, RAMDAC, and the X server to be used. Furthermore, some valuable information concerning the card is written to the device section in XF86Config.

If your card is not listed, do not panic. Switch back to the normal configuration by selecting ‘q’. Only select one of the defined cards if it matches your card exactly. Selecting a card with a similar name is not recommended. Similar names do not necessarily refer to similar hardware.

More information on how to configure your card is given in chapter *Section Optimizing the Installation of the X Window System* on page 160.

After specifying your card, the X server is next.

+   1. The XF86_Mono server. This is a monochrome server that should work on any VGA-compatible card, in 640x480 (more on some SVGA chip sets).
+   2. The XF86_VGA16 server. This is a 16 color VGA server that should work on any VGA-compatible card.
+   3. The XF86_SVGA server. This is a 256 color VGA server that supports a number of SVGA chip sets. It is accelerated on some Cirrus and WD chip sets. It supports 16 and 32-bit color on certain Cirrus configurations.
+   4. The accelerated servers. These include XF86_S3, XF86_Mach32, XF86_Mach8, XF86_8514, XF86_P9000, XF86_AGX, XF86_W32, and XF86_Mach64.

These four server types correspond to the four different "Screen" sections in XF86Config (vga2, vga16, svga, accel).

+   5. Choose the server from the card definition, XF86_S3.

Which one of these four screen types do you intend to run by default (1–4)?

# Output 8: Selecting the X Server

1. A server for monochrome (b/w) monitors. This should run on any VGA-compatible graphics card and at least offer a resolution of 640x480.

³Random Access Memory Digital-to-Analogue Converter.