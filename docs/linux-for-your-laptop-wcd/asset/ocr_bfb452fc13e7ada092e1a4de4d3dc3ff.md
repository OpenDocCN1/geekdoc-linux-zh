For example, after starting *minicom*, you should be able to type the `AT` command, press `Enter`, and then use the `AT^` command:

```
```
AT
OK
AT?
LP56OMX VER 2.01 V.90 (VER 1.14 TBR21 V.2)
OK
```
```

The first `OK` shows that your modem is responding. The `AT^` command “interrogates” your modem for manufacturer information.

# ## External Monitor Port

Few mid- to large-sized notebooks come without an external monitor or VGA port. This is a handy way to turn your notebook into a desktop system, especially if it has a diminutive screen or if you need a larger display with greater resolution than offered by the notebook’s LCD.

The safest procedure to follow when using an external display is to power down the computer, attach the monitor’s cable, and then restart. Although most notebooks have special `Fn` keyboard controls to toggle the display from LCD to monitor or both, you might need to enable external monitor use in your laptop’s BIOS. This is usually done by holding down a certain key or key combination just after you turn on your computer.

Don’t expect to be able to use the same color depth as your notebook when using higher resolutions on an external monitor. Color depth and resolution, as you’ve learned, are a function of the notebook’s graphics chipset and internal video memory. Most notebooks’ graphics memory is not adequate to support millions of colors at 1600×1200 pixels. When in doubt, check your laptop manual about connecting, configuring, and using an external display.

Mobile Linux users should be aware that in some instances, a particular graphics chipset might require particular settings in the system’s `XF86Config` file in order to display a running `X11` session on an external monitor. For example, if you have a notebook with a NeoMagic graphics chipset, and you want to display your `X` session on an external monitor, you’ll need to use this:

```
```
Option "extern_disp"
```
```

in the graphics device section of your `XF86Config` file. (Details are in the `README.neo` file under the `/usr/X11R6/lib/X11/doc` directory.)