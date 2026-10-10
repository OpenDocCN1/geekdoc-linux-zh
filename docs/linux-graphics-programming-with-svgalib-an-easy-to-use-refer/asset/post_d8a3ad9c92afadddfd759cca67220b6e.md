
published by the Free Software Foundation;
either version 2 of the License, or
(at your option) any later version.

This program is distributed in the hope that
it will be useful, but WITHOUT ANY WARRANTY;
without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR
PURPOSE. See the GNU General Public License
for more details.

You should have received a copy of the GNU
General Public License along with this
program; if not, write to the Free Software
Foundation, Inc., 59 Temple Place, Suite 330,
Boston, MA 02111-1307 USA

Also add information on how to contact you by electronic and paper mail.

If the program is interactive, make it output a short notice like this when it starts in an
interactive mode:

```
Gnomovision version 69, Copyright (C) 199y
name of author Gnomovision comes with
ABSOLUTELY NO WARRANTY; for details type
'show w'. This is free software, and you are
welcome to redistribute it under certain
conditions; type 'show c' for details.
```

The hypothetical commands 'show w' and 'show c' should show the appropriate parts of the
General Public License. Of course, the commands you use may be called something other
than 'show w' and 'show c'; they could even be mouse-clicks or menu items—whatever suits
your program.

You should also get your employer (if you work as a programmer) or your school, if any, to
sign a "copyright disclaimer" for the program, if necessary. Here is a sample; alter the names:

```
Yodopyne, Inc., hereby disclaims all copyright
interest in the program `Gnomovision'
(which makes passes at compilers) written
by James Hacker.

<signature of Ty Coon>, 1 April 1989
Ty Coon, President of Vice
```

This General Public License does not permit incorporating your program into proprietary
programs. If your program is a subroutine library, you may consider it more useful to permit
linking proprietary applications with the library. If this is what you want to do, use the
GNU Library General Public License instead of this License.

## Appendix B
## Libvga Functions

The material contained within this appendix was taken in large part from the man pages edited by Dr. Michael Weller (cowmob@exp-math.uni-essen.de). Unfortunately, the exact source of the original documentation has been lost with the passage of time. It's likely that at least some credit is due to Harm Hanemayer, whose last known email address was H.Hanemayer@inter.nl.net, but Hanemayer is believed to be offline now and thus unavailable for questioning.

Consequently, some of the newer SVGAlib man pages and HOWTOs were written by Matan Ziv-Av (matan@svgalib.org) and his contemporaries. In the event that credit has been wrongly applied, it's requested that notification be emailed to jlink@svgalib.org.

### Functions Defined In Vga.h

The libvga functions shown in this appendix are defined in vga.h, vgamoouse.h, vgakeyboard.h, and vgajoystick.h. These four SVGAlib header files can generally be found in the /usr/include or /usr/local/include directories.

### Initialization

The following functions pertain to initialization:

```c
int vga_init(void)
```

Detects the chipset and gives up supervisor rights. This is the recommended first line of any program that uses SVGAlib. vga_setchipset() can be called before it to avoid detection.

SVGA lib catches a bunch of signals that usually kill your program to restore text mode. If you catch signals before calling `vga_init()`, SVGAlib will restore text mode and prepare for shutdown and then call your handler routine. If you don’t want this, catch the signal after calling `vga_init()` and do not daisy-chain to SVGAlib’s original handler.

> **Warning**
> 
> SVGA lib needs two signals for its own purposes (that is, managing console switches). To avoid problems, it uses the otherwise unused signals SIGUSR1 and SIGUSR2. However, this means that you cannot use them in your program by any means. They are set up by `vga_init()`, as everything else is.

Since version 1.2.11, `vga_init()` includes code to hunt for a free virtual console on its own, in case you’re not starting the program from one (but instead over a network or modem login, from within “screen” or an “xterm”). Provided there’s a free console, this succeeds if you’re logged in as root or if the SVGAlib-calling user owns the current console. This is to avoid people not using the console being able to fiddle with it. Upon graceful exit, the program returns to the console from which it was started. Otherwise, it remains in text mode at the VC that SVGAlib allocated to allow you to see any error messages. In any case, any I/O the SVGAlib makes in text mode, after calling `vga_init()`, will also take place at this new console.

Alas, some games misuse their SUID root privilege and run as full root processes. SVGAlib cannot detect this and allows Joe Blow User to open a new VC on the console. If this annoys you, `ROOT_VC_SHORTCUT` in `Makefile.cfg` allows you to disable allocating a new VC for root (except for when root owns the current console) when compiling SVGAlib. This is the default (disabling the allocation for root).

`vga_init()` returns a nonzero value in case of errors. As of this writing, it will return -1 if it’s unable to allocate a graphical console. Otherwise, 0 is returned.

```c
void vga_disable_driverreport(void)
```

Usually SVGAlib prints the name of the hardware detected or forced to the screen during startup. This and other informational messages are suppressed when `vga_disable_driverreport()` is called.

```c
int vga_claimvideomemory(int m)
```

Declares the amount of video memory in bytes that’s to be saved when temporarily switching to text mode. Returns nonzero if the amount is not available. Defaults to one screen when a mode is set. Use this if you’re using more than one screen of video memory.

```c
void vga_safety_fork(void (*shutdown_routine)(void))
```

Calling this at the start of a program results in a better chance of text mode being restored in case of a crash. However, it has to raise the iopl (I/O privilege) level to 3 to work. This is a small security breach, because it’s passed on to any programs that you fork off. Bear in mind, however, that some SVGA card drivers have to use iopl() anyway. If you use it, call that function as the very first VGA function. Call it right before vga_init(). Note that `vga_safety_fork()` will already enter a graphics mode for font and graphics state saving. Don’t overestimate the power of this function: Your application will continue to run in the background while a foreground application will restore a usable screen and graphics mode in the event of a crash. The `forktest` demo shows the principal operation of this function.

**void vga_setchipset(int chipset)**

Forces detection of a chipset (when chipset detection fails). `vga_setchipset(VGA)` can be useful if the chipset-specific information or the SVGA-detection information gives you problems. However, the automatic detection should work well from the start, and if not, a specific chipset can be forced from `/etc/vga/libvga.config`. Because of this, `void vga_setchipset(int chipset)` should probably never be used by applications. If used, it should be called directly before `vga_init()`.

As of now, the following values are defined for *chipset*:

- **UNDEFINED**—This is the default. It specifies autodetection.
- **VGA**—A plain VGA card. This does not mean that the SVGA card will behave like an ordinary VGA card.
- **ET4000**—Tseng ET4000/ET4000W32(i/p) cards.
- **CIRRUS**—Cirrus Logic GD542x/3x cards.
- **TVGA8900**—Trident TVGA 8900C/9000 (and possibly also 8800CS/8900A/B cards).
- **OAK**—Oak Technologies OT1-037/67/77/87 cards.
- **EGA**—An ordinary EGA card. The notes about VGA apply.
- **S3**—An S3 base card.
- **ET3000**—Tseng ET3000 cards.
- **MACH32**—A card (not necessarily from ATI) based on the ATI Mach32 chipset.
- **GVGA6400**—A Genoa(?) GVGA6400 card.
- **ARK**—ARK Logic ARK1000PV/2000PV cards.
- **ATI**—An ATI SVGA (VGA coder and friends) card. This does not (necessarily) include the newer cards (usually called Mach something).
- **ALI**—An ALI2301-based card.
- **MACH64**—A card using the ATI Mach64 chipset. Support is not yet complete.
- **CHIPS**—Chips and Technologies chipsets 65525, 65535, 65546, 65548, 65550, and 65554 (usually found in laptops).
