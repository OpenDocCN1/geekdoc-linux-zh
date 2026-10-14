| Section | Description |
|---|---|
| **InputDevice** | Input devices are configured in this section. In contrast to XFree86-3.3, keyboards, mice, and special input devices (touch pad, joysticks, etc.) are configured via this section. Important terms here are Driver and the options defined by Protocol and Device. |
| **Monitor** | Describes the monitor used. The individual elements of this are the name, which is referred to later in the Screen definition, the bandwidth, and the allowed sync frequencies (HorizSync and VertRefresh). Settings are given in MHz, kHz, and Hz. Normally, the server refuses any mode line that does not correspond with the specification of the monitor. This is to prevent too high frequencies from being sent to the monitor by accident. |
| **Modes** | The mode line parameters are stored here for the specific screen resolutions. These parameters can be calculated by SaX2 on the basis of the values given by the user and normally do not need to be changed. You can intervene manually at this point, however, if, for example, you want to connect a fixed frequency monitor. An exact explanation of the individual parameters would be too much for this book. Find details on the meaning of individual number values in the HOWTO file `/usr/share/doc/howto/en/XFree86-Video-Timings-HOWTO.gz`. |
| **Device** | This section defines a specific graphics card. It is referenced by its descriptive name. |
| **Screen** | This section puts together a Driver (e.g., vga2), a monitor, and a Device to form all the necessary settings for XFree86. In the Display subsection, specify the size of the virtual screen (Virtual, the ViewPort, and the Modes) used with this virtual screen. |
| **ServerLayout** | This section defines the layout of a single or multihead configuration. The input devices InputDevice and the display devices Screen are combined into one section. |

*Table 7.4: Sections in `/etc/X11/XF86Config`*

We will now take a closer look at Monitor, Device, and Screen. Further information on the other sections can be found in the man page for XFree86 (man XFree86) and the man page for XF86Config (man XF86Config).