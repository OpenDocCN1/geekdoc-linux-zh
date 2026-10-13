# TABLE 3.1 CONTINUED

| File | Description |
|------|-------------|
| README.W32 | Notes for W32 and ET6000 chipset users |
| README.WstDig | Notes for Western Digital chipset users |
| README.agx | Information about the AGX XFree86 X server |
| README.apm | Notes about the Alliance Promotion chipset |
| README.ark | Notes for ARK Logic chipset users |
| README.ati | Information about XFree86's ATI Adapters video drivers |
| README.chips | Notes about Chips and Technologies chipsets |
| README.cirrus | Information about XFree86 support for Cirrus Logic chipset |
| README.clkprog | Programming info about external video clock setting programs |
| README.cyrix | Information about Cyrix chipsets |
| README.epson | Information about EPSON SPC8110 (laptop) chipsets |
| README.mouse | Details about XFree86's X11 mouse support |
| README.neo | Information about NeoMagic (laptop) chipsets |
| README.rendition | Information about the Rendition chipset |
| README.trident | Notes for Trident chipset users |
| README.tseng | Notes for Tseng chipset users |
| RELNOTES | Definitive release notes for XFree86 |
| ServersOnly | How your directories should look when building XFree86 X servers |
| VGADriver.Doc | HOWTO on adding an SVGA or VGA drive to XFree86 |
| VideoModes.doc | Eric S. Raymond's comprehensive treatise on building XF86Config modelines |
| xinput | General info on input device (such as joystick) support in XFree86 |

Before you use the xf86config command to reconfigure X11, log in as the root operator, and make a backup copy first, like so:

```
# cp /etc/XF86Config /etc/XF86Config.org
```

You can then start the command by typing it on the command line of a terminal window like this:

```
# xf86config
```