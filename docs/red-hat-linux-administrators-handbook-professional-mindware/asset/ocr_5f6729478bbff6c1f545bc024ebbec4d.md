# 1280x1024 @ 76 Hz, 81.13 kHz hsync
ModelLine "1280x1024" 135 1280 1312 1416 1664 1024
1027 1030 1064

EndSection

The following are the options in this section:

+   * **Identifier**. Used to set a unique identifier for the monitor. Each monitor needs to have a unique identifier that can be referenced in the Screen section.

+   * **VendorName** and **ModelName**. Used to specify the vendor name and model of the monitor.

+   * **HorizSync**. Used to set the horizontal refresh (sync) rate in kHz. If you want to specify this rate in megahertz or in hertz, use MHz or Hz, respectively, at the end of the line.

+   * **VertRefresh**. Used to set the vertical refresh (sync) rate in Hz. If you want to specify this rate in megahertz or in kilohertz, use MHz or kHz, respectively, at the end of the line.

+   * **Modeline**. Used to specify video modes. Each Modeline option has the following format:

```
Modeline mode clk-rate Horizontal-timing Vertical-timing Flags
```

+   * *clk-rate* is the rate of the pixel clock for this mode. This is a single positive (integer) number. *Horizontal-timing* and *Vertical-timing* are a set of four timing (integer) numbers. The *Flags* are optionally used to specify additional characteristics of the mode. A Modeline can be written in multiple lines using the *mod* option. For example:

```
Modeline "1024x768i" 45 1024 1048 1208 1264 768 776 784 817 Interlace
Mode "1024x768i"
DotClock        45
HTimings        1024 1048 1208 1264
VTimings        768 776 784 817
Flags           "Interlace"
EndMode
```