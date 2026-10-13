After you press Enter, follow the prompts to configure your graphics card and monitor for X11. The xf86config command generates a new XF86Config file in the /etc directory.

# The XF86Config File

The XF86Config file is used to properly feed font, keyboard, mouse, video chipset, monitor capabilities, and color depth setting information to your selected X11 display server. XF86Config is a single text file that consists of several sections that are summarized in Table 3.2.

You can page through your system's XF86Config file by using the less command (discussed in Hour 4, "Reading and Navigation Commands"). At the command line of a terminal, use less, followed by the path to XF86Config, like this:

```
# less /etc/XF86Config
```

You can then use the cursor keys to browse through the file. Press the Q key when you finish reading.

Table 3.2 Major Sections of the XF86Config File

| Section | Purpose |
|---|---|
| Files | Tells the X server where colors, fonts, or specific software modules are located |
| Module | Tells the X server what special modules should be loaded |
| ServerFlags | Contains on/off flags to enable or deny special actions, such as core dumps, keyboard server shutdown, video-mode switching, video tuning, and mouse and keyboard configuration |
| Keyboard | Tells the X server what keyboard to expect and what settings to use |
| Pointer | Tells the X server what pointer to use and how buttons are handled |
| Xinput | Special section for devices, such as graphics pads, styli, and so on |
| Monitor | Specifies details and settings for your monitor, such as name, horizontal sync ranges, vertical sync ranges, and modelines (one for each video resolution, such as 640x480, 800x600, 1024x768, and so on) |
| Device | Provides details about your video chipset, such as RAM, clockchips, and so on |
| Screen | Specifies what X server to use, the color depth (such as 8-, 16-, 24-, or 32-bits per pixel), screen size (such as 640x480, 800x600, 1024x768, and so on), and the size of the virtual screen |