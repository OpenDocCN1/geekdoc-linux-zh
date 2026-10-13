![](bbox=[0.14, 0.08, 0.22, 0.18])

> > The X Servers are based on the work of the XFree86 project. The server names reflect their video controllers. For example, you can assign the XF86_SVGA server to an SVGA card, the XF86_P9000 server to the Orchid P9000 card, and so on.

When you run SuperProbe, the utility warns you that it can make your computer hang. Within five seconds, your monitor screen may go blank as the utility probes your video hardware. If it detects the hardware you have, you'll see the results on your screen, as shown in Figure 10.1.

If you're setting up your configuration files without any of the other X Window configuration utilities, your next step is to link (ln) the X Server to the X command.

# xf86config

The xf86config utility is used at the command line to configure your video controller and monitor as well as your keyboard and mouse.

The xf86config utility represents one of the rare cases where graphical utilities are preferred. The lists used by xf86config are long and tedious. However, because it allows you to set your monitor and video controller settings from outside files, it's easier to keep this utility more up to date.

If you want more information on the available options at each step, review the next section on the XF86Setup utility. Although XF86Setup is a GUI utility, the options are nearly identical.

```
```
laptop:* SuperProbe
SuperProbe Version 2.20 (17 June 1999)
(c) Copyright 1993,1994 by David M. Eskelin <dave@xfree86.org>
(c) Copyright 1994-1998 by The XFree86 Project, Inc.

This work is derived from the "vgasetc.zip" and
"vga2cfg.zip" documentation packages produced by Finn
Thogerensen, and released with all appropriate permissions
having been obtained. Additional information obtained from
"Programmer's Guide to the EGA and VGA, 2nd ed." by Richard
Ferraro, and from manufacturer's data books

Bug reports are welcome, and should be sent to XFree86@XFree86.org.
In particular, reports of chipsets that this program is unable to
correctly detect are appreciated.

Before submitting a report, please make sure that you have the
latest version of SuperProbe (see http://www.xfree86.org/FAQ/).

WARNING - THIS SOFTWARE COULD HANG YOUR MACHINE.
READ THE SuperProbe MANUAL PAGE BEFORE
RUNNING THIS PROGRAM.

INTERRUPT WITHIN FIVE SECONDS TO ABORT!

First video: Super-VGA
Chips: Yamaha 2088 VESA VBE 3.0 (Port Probed)
RAMDAC: Generic 8-bit pseudo-color DAC
(with 8-bit wide lookup tables (or in 6-bit mode))

laptop:* 
```
```

Figure 10.1 The SuperProbe utility at work.