(Standard, Pro, Mobility). Cards based on these chip sets include All-in-Wonder 128, Rage Fury, Rage Magnum, Xpert 99, Xpert 128, and Xpert 2000.

+   - **3dfx** — If you can find a used unit on eBay, there are several 3dfx cards that support DRI. In particular, the Voodoo (3, 4, and 5) and Banshee chip sets have drivers that support DRI. Voodoo 5 cards support 16 and 24 bpp. Scan Line Interleaving (SLI), where two or more 3D processors work in parallel (to result in higher frame rates), is not supported for 3dfx cards.

+   - **3Dlabs** — Graphics cards containing the MX/Gamma chipsets from 3Dlabs have drivers available that support DRI in Linux.

+   - **Intel** — Supported video chipsets from Intel include the i810 (e, e2, and -dc100), i815 and i815e.

+   - **Matrox** — The Matrox chipsets that have drivers that support DRI include the G200, G400, and G450. Cards that use these chips include the Millenium G450, Millenium G400, Millenium G200, and Mystique G200.

+   - **NVIDIA** — Cards from NVIDIA are not supported by DRI because NVIDIA has not released hardware specifications to DRI developers. However, NVIDIA cards work for most Linux games. To get NVIDIA drivers, which are produced by NVIDIA but are not open source drivers, you must download them from the NVIDIA Web site (www.nvidia.com). On the NVIDIA home page, click the download button and follow the instructions for downloading and installing the correct drivers for your card. RPM packages are available.

To find out whether DRI is working on your current video card, type the following:

```
$ glxinfo | grep rendering
direct rendering: Yes
```

This example shows that direct rendering is supported. If it were not supported, the output would say No instead of Yes. Even if DRI is not supported, you may experience the best game play with a high-end card from either ATI or NVIDIA. While DRI support can be important, many games support OpenGL rendering, a feature supported by both NVIDIA and ATI video cards. Both companies have specific driver requirements, so make sure you research the cards, driver requirements, and any game-specific issue before you plonk down big money on a top-tier 3D video card.

# Running X Window Games

The X Window System created a great opportunity for games in Fedora and other UNIX systems to become graphical based rather than character based. So, instead of having little character symbols representing robots and arrows, the games could actually show pictures of little robots and arrows.