# ## Section “Device”

This section is where you configure your graphics adapter. Like most other sections, it begins with the keyword `Identifier`, followed by a name in quotes to identify the device. The `Driver` keyword is also required, followed by the name of the driver for your card in quotes. For example, if you have an NVIDIA TNT2, the line would look like this:

```
Driver “nv”
```

If you have a supported video card, it is much easier to go through `x86config` (explained earlier in this chapter) to set up the graphics device than to do it manually in the `XF86Config` file. However, if for whatever reason you need to or want to do it manually, a full list of the supported cards, along with the driver that should be used to support each card, is available at www.xfree86.org/current/Status.html.

The other keyword that is most commonly used here is the `VideoRam` keyword to specify how much video RAM the video card has. For example, if your video card has 16MB of RAM, the line would look like this:

```
VideoRam 16384
```

As you learned earlier, the amount of video RAM is specified in kilobytes; in binary math, a kilobyte is actually 1,024 bytes. Table 35.4 repeats the list of Video RAM values you saw earlier in Table 35.2; these numbers should be entered here for various amounts of video RAM.

TABLE 35.4 Video RAM in Megabytes and the Corresponding Kilobyte Values

| Video RAM in Megabytes | Amount of Memory in Kilobytes |
|------------------------|-------------------------------|
| 8                      | 8192                          |
| 16                     | 16384                         |
| 32                     | 32768                         |
| 64                     | 65536                         |
| 128                    | 131072                        |

Some more options are available for graphics devices, but most of them will not be needed for most video cards. See the man page for `XF86Config` for full details on all the available options.

Also, you will probably want to have a look at the Web page located at http://www.xfree86.org/4.0.2/index.html to see whether there are any notes regarding your particular type of video card and any specific options you need to supply for it.