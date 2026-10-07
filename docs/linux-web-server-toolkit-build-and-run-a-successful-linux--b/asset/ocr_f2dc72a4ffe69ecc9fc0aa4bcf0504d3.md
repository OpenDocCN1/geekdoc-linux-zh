# Linux Web Server Toolkit

on PCs) to emulate some functions of a three-button mouse (common on UNIX workstations). The section is as follows:

| Section Pointer |
| Protocol Microsoft |
| Device /dev/mouse |
| EndSection

# THE XF86CONFIG MONITOR SECTION

Things start getting more complicated in this section of XF86Config. The Monitor section contains definitions for one or more monitors, including an identifier, vendor name, model, and all the frequency values mentioned previously.
The most important part of the monitor section is the ModeLines. This series of lines defines how to create a certain resolution on the monitor by specifying the timing values for horizontal and vertical scanning. The problem is that you can't just make these up. If you can't get the configuration utility to create them for you, you should look for a sample file on the Internet that uses the same monitor model as yours. Copy the Monitor from that configuration file and insert it into yours.
Each ModeLine has a name, which is usually the resolution but can be anything (note it's in quotation marks). The dotclock specifies the timing base to be used on that line to generate the horizontal and vertical timing values to create that resolution. Each video card can generate certain dotclocks, as listed in the next section.
If you get the ModeLines correct, you won't damage your monitor because the X server won't try to send anything to the monitor that isn't listed here as a feasible option. The section is as follows:

| Section Monitor Primary Monitor |
| Identifier Unknown |
| VendorName Unknown |
| Model |
| HorSync 31.5-64.3 |
| VertRefresh 50-90 |
| Modeline 1152x864 64.97 1152 1168 1384 1480 864 865 875 985 interlace |
| Modeline 1024x768 75.00 1024 1048 1184 1238 768 771 777 806 |
| -hync -vsync |
| Modeline 800x600 50.35 800 856 976 1040 600 637 643 666 |
| +hync +vsync |
| Modeline 640x480 31.48 640 680 720 864 460 488 491 521 |
| EndSection

The Monitor section can have several monitors defined. That's why each one has an identifier line. The Screen section ("The XF86Config Screen section" later in the chapter) can then refer to a specific monitor by name. This also gives you some flexibility in having multiple hardware options supported by your system.