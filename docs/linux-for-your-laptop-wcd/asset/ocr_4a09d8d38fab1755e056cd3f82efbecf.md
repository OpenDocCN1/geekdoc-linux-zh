In this example, the database contains information that the NeoMagic card is not supported, and the script automatically chooses this vga X server module for the card. This example was used because there is a fix. Continue through the script to answer questions about video RAM, the default color depth (such as monochrome, 256, thousands of colors, or millions of colors). You’ll then see the following:

```
I am going to write the XF86Config file now. Make sure you don’t accidentally overwrite a previously configured one.

Shall I write it to /etc/X11/XF86Config?

Type a y and press Enter. At this point, most notebook users can try to start an X session using the startx command like this:

# startx
```

However, NeoMagic chipset users should edit the resulting /etc/X11/XF86Config file and then look for the first Driver entry:

```
Driver    "vga"
```

This should be changed to

```
Driver    "neomagic"
```

Next, look for the Device section’s Driver entry:

```
Driver    "vga"
```

This entry should be changed to

```
Driver    "neomagic"
```

Save the changes and exit your editor. You can then try to start your X11 session. This fix, which specifies that the X server module should load the neomagic.o server module instead of the designated vga.o module, should work with many different types of notebooks using NeoMagic graphics chipsets. The new set of graphics card server modules is installed under the /usr/X11R6/lib/modules/drivers directory:

```
aga_drv.o        fbdev_drv.o     neomagic_drv.o   tga_drv.o
ati_drv.o        glide_drv.o     nv_drv.o       trident_drv.o
chips_drv.o      glint_drv.o     r128_drv.o      tsecg_drv.o
cirrus_alpine.o  i740_drv.o     rendition_drv.o  vga_drv.o
cirrus_drv.o     i810_drv.o     svga_drv.o
cirrus_laguna.o  linix         sis_drv.o
cyrix_drv.o      mga_drv.o     tdfx_drv.o
```