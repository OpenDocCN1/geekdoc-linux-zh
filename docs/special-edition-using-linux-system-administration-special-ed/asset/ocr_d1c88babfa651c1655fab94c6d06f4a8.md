32 bpp is actually 24-bit color aligned on 32-bit boundaries. It does NOT mean the cards are capable of 32-bit color; they still display 24-bit color (16,777,216 colors). 24-bit packed pixels modes are not supported in XFree86, so cards that can do 24 bit modes to get higher resolutions in other OSes are not able to do this in X using XFree86. These cards include Mach32, Cirrus 542x, S3 801/805/868/968, ET4000, and others.

AGP (Accelerated Graphics Port) support is growing fast. Most of the X servers (both freely available and commercial versions) have more or less support for AGP.

# DIAMOND VIDEO CARDS

Most currently available Diamond cards are supported by the current release of XFree86. Early Diamond cards may not be officially supported by XFree86, but there are ways of getting them to work. Diamond is now actively supporting the XFree86 Project.

# SVGALIB (GRAPHICS FOR CONSOLE)

+   - VGA
+   - EGA
+   - ARK Logic ARK1000PV/2000PV
+   - ATI VGA Wonder
+   - ATI Mach32
+   - Cirrus 542x, 543x
+   - OAK OTI-037/67/77/87
+   - S3 (limited support)
+   - Trident TVGA8900/9000
+   - Tseng ET3000/ET4000/W32

# XFREE86 3.3.2

# ACCELERATED

+   - ARK Logic ARK1000PV/VL, ARK2000PV/MT
+   - ATI Mach8
+   - ATI Mach32 (16 bpp supported for cards with RAMDAC ATI68875, AT&T20C49x, BT481 and 2MB video ram)
+   - ATI Mach64 (16/32 bpp supported for cards with RAMDAC ATI68860, ATI68875, CH8398, STG1702, STG1703, AT&T20C408, 3D Rage II, internal, IBM RGB514)
+   - Chips & Technologies 64200, 64300, 65520, 65525, 65530, 65535, 65540, 65545, 65546, 65548, 65550, 65554
+   - Cirrus Logic 5420, 542x/5430 (16 bpp), 5434 (16/32 bpp), 5436, 544x, 546x, 5480, 62x5, 754x