**Table F.29 Changes in 1.01 (date unknown).**

| Programmer | Contribution |
| :--- | :--- |
| Unknown | • Fixed copying to planar 256-color mode in **vgagl** and added page-flipping support. Setting an SVGA mode after a planar 256-color mode clears the screen properly now. Shared library 1.0.10. |

**Table F.30 Changes in 1.00 (January, 1994).**

The version number doesn’t say anything about stability/completeness, and so on.

| Programmer | Contribution |
| :--- | :--- |
| Unknown | • A number of bug fixes related to Mode X (display start, console switching, and planar 320x200x256 allowed with **vga_setmodex**()). | 
| | • Added **vga_copyplanar256** for Mode X-like modes. Added smooth scrolling demo program. Demo programs moved to **demos/**. | 
| | • Cirrus linear addressing works (if you have less than 16MB of memory); see **demos/testlinear**. Added ET3000 driver. Trident 8900 reboot-beep problem should be fixed. | 
| | • Shared library 1.0.9. |

**Table F.31 Changes in 0.99 (date unknown).**

| Programmer | Contribution |
| :--- | :--- |
| Unknown | • ET4000 patches by Hartmut Schirmer: ET4000 register dumps now have extra registers, so old register dumps won’t work. Register dump program (**tseng3**, moved to **et4000/** directory) supports VESA modes. Microsoft mouse handling bug fixed. Shared library 1.0.8. |

**Table F.32 Changes in 0.98 (date unknown).**

| Programmer | Contribution |
| :--- | :--- |
| Unknown | • Some minor bug fixes and low-level mouse handling rewritten (was very slow). | 
| | • Added **vga_runinbackground**() and **vga_oktowrite**() as a kludge to allow a graphics program to run in the background (not entirely safe). | 
| | • Disabled ET4000 clock detection (wasn’t used yet). | 
| | • Shared library version 1.0.7. |

**Table F.33 Changes in 0.97 (date unknown).**

| Programmer | Contribution |
| :--- | :--- |
| Unknown | • Fixed Cirrus 1,024x768x256 noninterlaced. Other modes use default (lowest) frequencies. Fixed bad virtual screen bug in **vgagl** (**copyscreen**). | 
| | • Incorporated patches from Hartmut Schirmer (et4000 clock frequency determination). | 
| | • Shared library 1.0.6. |