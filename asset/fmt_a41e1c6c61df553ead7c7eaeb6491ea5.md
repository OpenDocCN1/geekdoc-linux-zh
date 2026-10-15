
### The XF86 Servers

1. The `XF86_Mono` server. This is a monochrome server that should work on any VGA-compatible card, in 640x480 (more on some SVGA chip sets).

2. The `XF86_VGA16` server. This is a 16 color VGA server that should work on any VGA-compatible card.

3. The `XF86_SVGA` server. This is a 256 color VGA server that supports a number of SVGA chip sets. It is accelerated on some Cirrus and WD chip sets. It supports 16 and 32-bit color on certain Cirrus configurations.

4. The accelerated servers. These include `XF86_S3`, `XF86_Mach32`, `XF86_Mach8`, `XF86_8514`, `XF86_P9000`, `XF86_AGX`, `XF86_W32`, and `XF86_Mach64`.

These four server types correspond to the four different "Screen" sections in `XF86Config` (vga2, vga16, svga, accel).

5. Choose the server from the card definition, `XF86_S3`.

Which one of these four screen types do you intend to run by default (1–4)?

### Output 8: Selecting the X Server

1. A server for monochrome (b/w) monitors. This should run on any VGA-compatible graphics card and at least offer a resolution of 640x480.

2. 16 color server `XF86_VGA16`. Should run with any VGA-compatible card.

3. SVGA server `XF86_SVGA`. This server supports a wide variety of SVGA cards. Graphics acceleration is used with some Cirrus or WD cards. The 16- or 32-bit color mode can be activated with some Cirrus cards.

4. Server for accelerated cards (see below).

5. This item only exists if you have entered a card definition in the previous selection. Here, the server is selected (default) that suits the selected card.

When you have selected a server, you are asked if you want to create a symbolic link to `/usr/X11R6/bin/X`. If you answer with 'y', you are asked whether you want to put it in `/var/X11R6/bin/X`.

Do you want to set it in `/var/X11R6/bin`?

Reply with 'y', since it may not always be possible to write to `/usr` tree.

Afterwards, if you have selected '4' (the accelerated servers) in the previous selection, a menu is presented of all available accelerated X servers.

Select an accel server:

| Choice | Server |
| --- | --- |
| 1 | `XF86_S3` |
| 2 | `XF86_Mach32` |
| 3 | `XF86_Mach8` |
| 4 | `XF86_8514` |
| 5 | `XF86_P9000` |
| 6 | `XF86_AGX` |
| 7 | `XF86_W32` |
| 8 | `XF86_Mach64` |

Which accel server:

These servers support each card listed above. To create links, the appropriate server must already be installed. This means that you must already have selected the correct server during the installation of your X Window System. After selecting your X server, configure your graphics. First, specify the amount of memory the video card has.

How much memory do you have on your graphics card:

| Choice | Memory |
| --- | --- |
| 1 | 256K |
| 2 | 512K |
| 3 | 1024K |
| 4 | 2048K |
| 5 | 4096K |
| 6 | Other |

Enter your choice:

### Output 9: Specifying the Video Memory

Next, enter the name, vendor name, and type for your graphics card. If you earlier selected a card from the predefined list, pressing `↵` will enter this as the default.

```
Enter an identifier for your graphics card definition:

Enter the vendor name of your graphics card:

Enter the model (board) name of your graphics card:
```

If you chose an accelerated X server, you must enter the RAMDAC settings. This only applies to the S3 and AGX servers.

| Choice | RAMDAC | Identifier |
| --- | --- | --- |
| 1 | AT&T 20C490 (S3 server) | `att20c490` |
| 2 | AT&T 20C498/21C498/22C498 (S3) | `att20c498` |
| 3 | AT&T 20C505 (S3) | `att20c505` |
| 4 | BrookTree BT481 (AGX) | `bt481` |
| 5 | BrookTree BT482 (AGX) | `bt482` |
| 6 | BrookTree BT485/9485 (S3) | `bt485` |
| 7 | Sierra SC15025 (S3, AGX) | `sc15025` |
| 8 | S3 GenDAC (86C708) (autodetected) | `s3gendac` |
| 9 | S3 SDAC (86C716) (autodetected) | `sdac` |
| 10 | STG-1700 (S3) | `stg1700` |
| 11 | TI 3020 (S3) | `ti3020` |
| 12 | TI 3025 (S3) | `ti3025` |
| 13 | TI 3020 (S3, autodetected) | `ti3020` |
| 14 | TI 3025 (S3, autodetected) | `ti3025` |
| 15 | TI 3026 (S3, autodetected) | `ti3026` |
| 16 | IBM RGB 514 (S3, autodetected) | `ibm_rgb514` |
