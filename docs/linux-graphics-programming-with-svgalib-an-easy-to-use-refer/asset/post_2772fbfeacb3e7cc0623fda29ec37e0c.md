
## Table F.10 Changes in 1.27 (August 21, 1995).

| Programmer | Contribution |
| :--- | :--- |
| Michael Weller<br>(eowmob@exp-math.uni-essen.de) | • Mach32-related changes:<br>• Cosmetic fixes.<br>• New config commands svgaclocks.<br>• RAMDAC.<br>• Vendor to help support alien (not conforming to original ATI specs) cards (should work for Dell now).<br>• Fixed several NULL ptr dereferences that dclked under ELF. |
| David Mosberger-Tang<br>(davidm@azstarnet.com) | • Patches to make SVGAlib work on Linux/Alpha. (Only known to work with #9 GXE PCI; other cards might not work.) |
| Harm Haanemayer<br>(hhanaemaa@cs.ruu.nl) | • Changed duplicate include check vgmouse.h.<br>• Fixed bug in gl_getpixelo() in 3-bytes-per-pixel modes.<br>• Allowed Ctrl-C detection to be disabled in raw keyboard interface. |
| Gregory Margo<br>(gmargo@newton.vip.best.com) | • Support for the Logitech Mouseman mouse series.<br>• Override mouse mode from environment (SVGA_MOUSE_OVERRIDE). Useful for Doom. |
| Stephen Lee<br>(sl14@cruix1.cit.cornell.edu) | • ELF support.<br>• Countless patches for code cleanup.<br>• Bug fixes in S3 15/16/24bpp.<br>• Autodetection for more chips (but, alas, no support for them). |
| Michael Weller<br>(eowmob@exp-math.uni-essen.de) | • Moved config files to /etc/vga due to requests.<br>• Patched Makefiles for automatic reconfiguration. |

## Table F.11 Changes in 1.26 (April 27, 1995).

| Programmer | Contribution |
| :--- | :--- |
| Unknown | • Really fixed console switching in raw keyboard mode.<br>• Fixed SDAC support.<br>• Fixed Trio64 detect. Modes don't work though (use RAMDAC "normal").<br>• Moved ET4000 chip-type detection so that it works when the chip sets forced in the config file.<br>• Fixed Cirrus 5420/22/24 support.<br>• Mach32-related changes: Minor typos in mach32info fixed. 68800-6 should now be reported correctly. Fixed compiler warnings in mach32.c due to changed interface (no new accel interface yet). NewLAG for red first in 24bpp returned for Mach32 with DAC 4.<br>• Support for 24bpp red first in whole svgalib + vgagl.<br>• Added support for 32bpp in vgadraw.c.<br>• Added detection for 24bpp red first in vgatest.<br>• TODO—Fix raw keyboard console switching when Alt is kept pressed (for example, in Doom). |

## Table F.12 Changes in 1.25 (March 7, 1995).

| Programmer | Contribution |
| :--- | :--- |
| Unknown | • Problem with programs that don’t call vga_init finally fixed.<br>• Fixed console switching in svga/lm raw keyboard mode (**vgakeyboard.h**).<br>• Working **ARK** driver (includes acceleration).<br>• Linear addressing detection changed (supports partial frame-buffers).<br>• Added more **RAMDAC** support—AT&T490-compatible true-color DACs supported for S3.<br>• Tweaked mouse/keyboard header files to fix conflict with **libgrx** compile. |

## Table F.13 Changes in 1.24 (date unknown).

| Programmer | Contribution |
| :--- | :--- |
| Unknown | • Fixed bug causing “not running in ...” messages if **vga_init** wasn’t called.<br>• Better structure for driver interface (“DriverSpecs”). Fields other than the basic driver functions can be included. Type checking is also better. Most drivers haven’t been updated for the new return types; feel free to send patches. Something might be broken. Watch out.<br>• Better acceleration interface.<br>• Fixed **ARK** chip-type detection.<br>• Better **ARK** chip support.<br>• Largely fixed S3-864 and **SDAC** support.<br>• Untested clock/**DAC** support for the Trio64 in the S3 driver.<br>• Unlocked extended registers when forcing Cirrus in config file.<br>• Try to avoid Cirrus hardware lockup when switching certain modes.<br>• Added “accele” program to test new acceleration interface. |

## Table F.14 Changes in 1.23 (February 8, 1995).

| Programmer | Contribution |
| :--- | :--- |
| Unknown | • ET4000/W32 tweaks.<br>• Added **gl_allocatecontext()**. Use this instead of declaring **GraphicsContext** variables statically. Demo programs changed accordingly.<br>• Safer VC switching with bits.<br>• Allowed Cirrus SVGA modes with 512K memory.<br>• Possible Cirrus 5422 MCLK detection fix.<br>• Incorporated ATI “drive” from Scott Heavner (allows VGA with 132-column text mode).<br>• Untested **ARK** driver and untested generic S3 support (640×480×256 at 60Hz).<br>• Unused acceleration interface sketch (accel/h/cirrus.c). |

## Table F.15 Changes in 1.22 (date unknown).

| Programmer | Contribution |
| :--- | :--- |
| Unknown | • ET4000 additions for STG170X **DAC** (tseng3.c and driver), linear addressing support for W32p, better general linear addressing handling with new driver function, 8-bit color components CLUT support for AT&T **DAC** (David Etherton).<br>• Cirrus driver tweaks.<br>• S3 driver rewritten for S3-864 and **SDAC** (doesn’t work yet) using new interface.<br>• Linear addressing probing with **vga_setlinearaddressing**. Console switching is not a good idea with linear addressing enabled.<br>• Treat Oak 077 as standard **VGA** (incompatible with OTI-087 mode dumps).<br>• Fixed planar **gelpixel** (untested).<br>• VC switching in raw keyboard mode (for example, Doom) (doesn’t always work) (was typo, fixed in 1.25).<br>• **VGAGLI** status—Should be usable separate from SVGAlib with minor changes. **GraphicsContext** should be allocated dynamically (**malloc**) by library for compatibility/extensibility. Nonstandard font text write functions added (untested). Missing proper direct page flipping support (double-buffering in video memory). This would require all operations to be performed at a certain offset into the frame buffer. |

## Table F.16 Changes in 1.21 (December 23, 1994).

| Programmer | Contribution |
| :--- | :--- |
| Unknown | • Partially restructured Cirrus driving using clean, XF86e86-style **SVGA** generalized interface. Check out **timing.*, vgares.*,** and **circus.c.**<br>• Cirrus driver **init** should now support all 542x/543x cards.<br>• Fixed **MouseSystems** movement overflow.<br>• Fixed PS/2 mouse support (finally. Sorry).<br>• Fixed (old) Logitech protocol mouse handling (hopefully—I lost the message that contained the fix).<br>• Fixed Cirrus **bitblt** bug.<br>• Gvga6400 driver BIOS check changed; **munmap** seems to mess things up.<br>• Added **vga_gelpixel()** (untested).<br>• Incorporated **restorepalette** patch from Charles Blake, which allows custom text mode console colors (see **utils/README**). |
| Michael Weller<br>(eowmb@exp-math.uni-essen.de) | • Made **CGVGA MODE** parsing case insensitive and added names for 16M32 modes.<br>• **Vgatest** displays info about 16M32 modes better.<br>• Mach32—Support for 8-bit **CLUT** on Type 2 DACs.<br>• Added **testaccel** demo.<br>• Mach32—Support for all accelerator functions.<br>• Added **vga_hlineint()**, **vga_blwait()**, **vga_rs_ext()**, and **vga_accel()**.<br>• Mach32—**EEPROM** interpretation more robust and configurable for stupid AST boards.<br>• Mach32—changed **16M4 -> 16M32** for compatibility.<br>• Fix: reserve memory for one screen on **EACH** setmode call (as the **README** states).<br>• Mach32—Added support for AST-style **EEPROM** checksums.<br>• Added commands to control **RTS/DTR** lines for multiprotocol mice.<br>• Fix: Mach32—VGA modes should work now even in 132-column text modes.<br>• Sanity check for **MAX_REGS** in **vga.c**.<br>• Fix: Raised **MAX_REGS** as was actually needed.<br>• Fix: Text mode utils now give errors on problems with accessing files.<br>• Fix: Restore of Mach32 regs after clock probe was broken (cosmetic; no problems reported).<br>• Fix: Mach32 **DAC1&4** have to use double/triple clocks in 16/24bpp.<br>• Cleaned up **VT** code a bit.<br>• Slight **ET4000/W32p** detection fix.<br>• Possible Mach32 32bpp **copy screen** fix.<br>• Allowed **VT** switching with mouse support (it was disabled because of interaction with an old version of selection, I take it things are better now?).<br>• Preliminary Cirrus 5434 support (untested, only 1,280x1,024x256 for now). Will be fixed soon.<br>• New **Oak** driver (Christopher Wiles).<br>• Used **seteuid** instead of **setuid** to give up **setuid-root** permissions.<br>• Hack that may fix 132-column text mode/VGA problems on **ET4000**.<br>• Fixed color/mono config option (mono was broken).<br>• Disabled 320x200x56 page flipping for **ET4000**.<br>• Fixed Cirrus **fillbt** register corruption problem.<br>• **GVGA6400** driver (Arno Schafer).<br>• **Vga_init()** now returns -1 if not on a suitable console (0 otherwise); hard exit can only happen in **vga_setmode()** (David Liu). This should help programs with multiple output devices such as **gnuplot**.<br>• Added **mouse_init_return_fd** and **keyboard_init_return_fd** for **select()** use.<br>• Added **SIGKILL** catch to raw keyboard interface.<br>• PS/2 mouse support possibly fixed.<br>• Shared library **1.2.0** (corresponds with main **SVGAlib** version number).<br>• Delayed console checking until actually setting a mode (should fix problems with device-probing programs such as **gnuplot**).<br>• Fixed planar mode **getmode** bug for Trident and others (should fix floating-point exceptions in **zgv**).<br>• Supported PS/2 mouse in config file.<br>• Fixed one-byte-per-pixel **gl_putxoremask**.<br>• Shared library **1.1.8**. |
