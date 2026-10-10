
The first three lines you are concerned about are the ones that begin with `Identifier`, `VendorName`, and `ModelName`. These lines identify the type of monitor this section is for. Look for the vendor name and model of your monitor in these lines.

The final two lines you are concerned with are the ones that begin with `HorizSync` and `VertRefresh`. If you find a section for your monitor, write down these two values for use in the configuration; then select 11 and enter the horizontal sync rate you wrote down. If you can't find this information in your monitor's manual, and you can't find an entry in the Monitors file, select one of the predefined entries where the listed resolution and refresh rate does not exceed a refresh rate you know your monitor can handle.

> **TIP**
>
> Many hardware vendors are now making documentation and technical specifications for their products that are available online at their Web sites. If you can't find the printed documentation for your monitor, it might be worth a trip to the vendor's Web site to see whether it has documentation and technical specifications available online.

Once you have selected one of the predefined entries or entered your monitor's horizontal sync range, press Enter to move to the next screen, where you will be asked to set the vertical refresh rate:

You must indicate the vertical sync range of your monitor. You can either select one of the predefined ranges below that correspond to industry-standard monitor types, or give a specific range. For interlaced modes, the number that counts is the high one (e.g. 87 Hz rather than 43 Hz).

- 1 50-70
- 2 50-90
- 3 50-100
- 4 40-150
- 5 Enter your own vertical sync range
- Enter your choice:

Once again, it is very important that you do not select a refresh rate higher than your monitor can handle; otherwise, you may cause damage to your monitor. If you know the vertical refresh rate for your monitor, select 5 and then enter the refresh range for your monitor. Otherwise, you can select 1-4 for one of the predefined types. Press Enter after you have made your selection to continue on to the next screen:

You must now enter a few identification/description strings, namely an identifier, a vendor name, and a model name. Just pressing enter will fill in default names.

The strings are free-form, spaces are allowed.

Enter an identifier for your monitor definition:

This is the information that will show up in the XF86Config file that the program will generate after you have finished entering all the values. You can just press Enter here to accept the defaults.

## Configuring the Video Card

Next, you will be given some information about configuring the video card. Press Enter after you have read the information to get to the card database. It will look like the following:

```
0  2 the Max MAXColor S3 Trio64V+ S3 Trio64V+
1  2-the-Max MAXColor 6000 ET6000
2  3DLabs Oxygen GMX PERMEDIA 2
3  928Movie S3 928
4  AGX (generic) AGX-014/15/16
5  ALG-5434(E) CL-GD5434
6  AOpen PA2010 Voodoo Banshee
7  ASUS 3Dexplorer RIVA128
8  ASUS PCI-AV264CT ati
9  ASUS PCI-V264CT ati
10 ASUS Video Magic PCI V864 S3 864
11 ASUS Video Magic PCI VT64 S3 Trio64
12 AT2S Alliance AT3D
13 AT3D Alliance AT3D
14 ATI 3D Pro Turbo ati
15 ATI 3D Pro Turbo PC2TV ati
16 ATI 3D Xpression ati
17 ATI 3D Xpression+ ati
```

Enter a number to choose the corresponding card definition.

Press enter for the next page, q to continue configuration.

Once again, there are many more cards listed in the database than can fit on one screen. Press Enter to get to the next page. When you reach the end of the list, pressing Enter will start the list over at the first page.

If you can't find your video card in this list, simply press Q to quit. Don't select a model just because it looks similar, because this could cause problems. Models that have similar names do not necessarily have similar hardware.

If you do find the make and model of your video card in the list, enter its number and then press Enter. You will then receive information about the video card you selected. Here's an example:

```
Your selected card definition:

Identifier:  Matrox Millenium G400
Chipset:  mgag400
Driver:  mga
Do NOT probe clocks or use any Clocks line.
```

```
Press enter to continue, or ctrl-c to abort.
```

Pressing Enter here will continue on to the next question. Pressing Ctrl+C will abort the entire program and cancel the configuration. If you do this, you will have to rerun xf86config and start over.

After you press Enter to continue, you are asked to give some more information about your video card, starting with the amount of RAM it contains:

Now you must give information about your video card. This will be used for the "Device" section of your video card in XF86Config.

You must indicate how much video memory you have. It is probably a good idea to use the same approximate amount as that detected by the server you intend to use. If you encounter problems that are due to the used server not supporting the amount of memory you have (e.g. ATI Mach64 is limited to 1024K with the SVGA server), specify the maximum amount supported by the server.

```
How much video memory do you have on your video card:

1  256K
2  512K
3  1024K
4  2048K
5  4096K
6  Other
```

```
Enter your choice:
```

Unless you have a very old video card, you probably have more RAM than any of the default options here, so you will want to select 6 and then enter the amount of RAM manually.

If you do this, you will be asked to enter the amount of video RAM installed in the system in kilobytes. Remember that in binary math, a kilobyte is equal to 1,024 bytes, not 1,000 bytes. Table 35.2 shows the value to enter for various amounts of video RAM.

**TABLE 35.2** Video RAM in Megabytes and the Corresponding Kilobyte Values

| **Video RAM in Megabytes** | **Amount of Memory in Kilobytes** |
| :--- | :--- |
| 8 | 8192 |
| 16 | 16384 |
| 32 | 32768 |
| 64 | 65536 |
| 128 | 131072 |

Enter the number under Amount of memory in Kbytes and then press Enter to continue on to the next screen:

> You must now enter a few identification/description strings, namely an identifier, a vendor name, and a model name. Just pressing enter will fill in default names (possibly from a card definition).
>
> Your card definition is Matrox Millennium G400.
>
> The strings are free-form, spaces are allowed.
> Enter an identifier for your video card definition:

If you selected a video card type from the card list, there will already be a suggested identification/description string listed here. I suggest that you accept the default that is given. If you can't find your card in the list, enter a description of your video card here and then press Enter.

Depending on whether or not you selected a card definition from the database, you will be presented with a different set of questions. Read the appropriate upcoming section, depending on whether you did or did not select a card definition from the database.

## Selecting a Card from the Database and Saving the Configuration File

If you selected a card definition from the database list, you will be presented with a menu of currently configured video modes. The following shows an example of what this might look like:

For each depth, a list of modes (resolutions) is defined. The default resolution that the server will start-up with will be the first listed mode that can be supported by the monitor and card. Currently it is set to:

```
"640x480"  "800x600"  "1024x768"  "1280x1024"  for 8-bit
"640x480"  "800x600"  "1024x768"  "1280x1024"  for 16-bit
"640x480"  "800x600"  "1024x768"  "1280x1024"  for 24-bit
```

Modes that cannot be supported due to monitor or clock constraints will be automatically skipped by the server.

- 1.  Change the modes for 8-bit (256 colors)
- 2.  Change the modes for 16-bit (32K/64K colors)
- 3.  Change the modes for 24-bit (24-bit color)
- 4.  The modes are OK, continue.

Enter your choice:

You will probably want to make some changes here because, by default, X-Windows will start up in a resolution of 640×480, which is virtually unusable. If you have a 17-inch monitor, you will probably want to go with at least 1024×768, and you may want to go even higher. If you have a 19- or 21-inch monitor you can definitely go higher than 1024×768. If you have a 15-inch monitor, you might want to try 1024×768, but this might be too small and you will have to go down to 800×600. If you have a 14-inch monitor, 1024×768 will likely be too small, and you will want to go down to 800×600 or possibly even stay with 640×480.

Also, you will want to decide what color depth to use. As a general rule, the higher the color depth, the better. If you have a small amount of video RAM, though, color depth and resolution may be a tradeoff. In general, you will not notice a difference in most applications between 16-bit and 24-bit color. However, there will be a big difference between 8-bit color and 16-bit color. Although personal preference has to be the governing factor, here are my recommendations:

- If the resolution you want to run does not allow more than 8-bit color (256 colors), it is probably better to reduce the resolution to a level that allows 16-bit color. However, if getting more than 256 colors requires you to reduce the resolution to a value lower than 1024×768, you may want to reconsider this.
- If the resolution you want to run does allow 16-bit color but does not allow 24-bit color, it is probably not worth reducing the resolution to allow 24-bit color. In most cases, unless you are doing something in which the number of colors is extremely important, you are not likely to notice a huge difference between 16-bit and 24-bit color.
