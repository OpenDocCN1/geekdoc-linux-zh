# LISTING 4.4 CONTINUED

| SampleRate | 60 |
| --- | --- |
| BaudRate | 1200 |
| EndSection | |

# XF86Config Monitor Section

The first parts of the sax-generated XF86Config file are easy to understand, but many Free86 users whose initial XF86Config file does not work until you pay attention to the Monitor section (a sample for an 800 × 600 laptop is shown in Listing 4.5), the Device section (Listing 4.6) and the Screen section (Listing 4.7). The Monitor section contains specific details and settings for your monitor, such as your monitor's name, its horizontal and vertical sync ranges, and critical modelines (one for each video resolution—example, 640 × 480, 800 × 600, 1,024 × 768). Understanding the modeline is key to fine-tuning your X11 display.

> Note
If you choose to use another tool, such as XF86Setup, or the xf86config command to create your XF86Config file, the content and listing file will be quite different from those in this section. However, your XF86Config file will work just as well.

For the best details, see the VideoModes.doc and README.Config files under the /usr/X11R/lib/X11/doc directory before fine-tuning modelines in your XF86Config file. Another good tutorial is the XFree86-Video-Timings-HOWTO under the /usr/doc/howto directory.

The basic parts of a modeline are 10 different values representing (from left to right)

+   - A label of the screen resolution, such as 800 × 600
- A driving clock frequency in MHz
- The number of visible dots per line on your display
- The Start Horizontal Retrace value (number of pulses before video sync pulse starts)
- The End Horizontal Retrace value (end of sync pulse)
- The total number of visible and invisible dots on your display
- The Vertical Display End value (number of visible lines of dots on your display)