# Table 11-3

# ## Boot Options to Fix Video Problems

| Option | Result |
| --- | --- |
| knoppix noddc | No Display Data Channel (DDC) detection of monitor. |
| knoppix screen-=?? | Pick X screen resolution. ?? with 640 × 480, 800 × 600, 1024 × 768, 1280 × 1024, or any other resolution supported by your video card. |
| knoppix xvrefresh=60 | Set vertical refresh rate to 60 Hz for X (or other value specified by monitor's manual). |
| knoppix xrefresh=80 | Set horizontal refresh rate to 80 Hz for X (or other value specified by monitor's manual). |
| knoppix xserver=?? | Replace ?? with XFree86 or XF86_SVGA. |
| knoppix xmodule=?? | Select the specific driver to use your video card. ?? with one of the following: ati, fbdev, i180, mga, nv, radeon, savage, s3radeon, svga, or i180. |
| knoppix 2 | Runlevel 2, Text mode only. |
| knoppix vsga=normal | No-framebuffer mode, but X. |
| knoppix fb1280x1024 | Use fixed framebuffer graphics (1). |
| knoppix fb1024x768 | Use fixed framebuffer graphics (2). |
| knoppix fb800x600 | Use fixed framebuffer graphics (3). |

# ## Customizing KNOPPIPIX

Several boot options exist that tell KNOPPIPIX to look for a customized directory or configuration information on hard disk or floppy. See the “Keeping Your KNOPPIPIX Configuration” section in this chapter for information on how to save a customized KNOPPIPIX configuration and tell KNOPPIPIX where to look for that customized information at boot. (Unless they were created from KNOPPIPIX, other Linux distributions will not use these boot options.)

# ## Special Features and Workarounds

Other boot options are described in the knoppix-cheatcodes.txt file mentioned earlier. Things you can do with boot options include changing the splash screen when KNOPPIPIX boots, in expert mode so you can load your own drivers, testing your computer’s RAM, and trying to overcome special problems with laptop computers.