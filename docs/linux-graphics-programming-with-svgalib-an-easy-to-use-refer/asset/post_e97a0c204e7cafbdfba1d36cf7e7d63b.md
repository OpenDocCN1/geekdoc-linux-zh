
## Other Elements

Other common elements of a GUI include scrollbars and icons, in addition to menus and pop-up display boxes. Believe it or not, these are actually very easy to program. Any sort of document or screen sliding can be achieved in a manner consistent with an arcade game that allows background scrolling. Similarly, screen icons are very much akin to the sprites found in these same games, as they can be moved around the desktop, and a timer is required to assess double clicks. For this reason, the best tutorials for scrollbars and icons will be Chapter 10, Basic Animation, and Chapter 14, Game Basics.

For your convenience, examples of complete GUIs can be found on the SVGAlib Web site at www.svgalib.org.

## Conclusion

The graphical user interface is definitely the wave of the future, even with the Linux crowd. Although many GUIs are already in place, designers must strive to continue making improvements in usability, functionality, and convenience. After all, there's nothing worse than a sloppy and/or ineffective interface—you can just hear your users running back to the command line.

One popular, emerging trend is to combine several interfaces into one. When done correctly, this gambit can make life easier on the end user. An application might serve as a Web browser, word processor, and desktop environment, all fused together to form the ultra-layout of tomorrow. Of course, some companies have already attempted this, but the results have been less than ideal, thus bringing back fond memories of shell prompts.

The important thing to remember is to take your time and do it right. Companies that care spend an enormous amount of time testing new interfaces, both with their own employees and with the general public. If you can remember to keep the end user in mind, your interface should emerge to become both pleasing and useful, which is, of course, the ultimate goal.

## Summary Of Functions Introduced In This Chapter

The following function was covered in this chapter:

- `void gl_setwritemode(int m)`

## Chapter 20 Video Card Drivers

**Key Topics:**
- **What’s a driver?**
- **Assembling your driver**
- **Debugging**

One of the most commonly asked questions regarding SVGAlib is, when will a driver be written for my hardware? Ironically, the answer is usually, “When someone who owns your type of display adapter writes one.” This sort of exchange leaves most users exasperated, and progress is rarely made.

The problem isn’t a matter of laziness, as one might expect. After all, SVGAlib people love to code. Rather, the truth is more along the lines of simple ignorance—most people have absolutely no idea where to begin. Coding a new driver isn’t a simple matter of “just doing it” but rather one of knowledge and experience. What’s more, there aren’t a whole lot of tutorials floating around the Net, either.

Here, then, will be a driver programming overview. Although this chapter won’t make you an instant expert on direct VGA card access, it’ll definitely get you started off on the right foot. And, if it’s any consolation, previous experience with hardware programming isn’t a prerequisite (although it certainly doesn’t hurt). You can cut your teeth here, and there’s room to make mistakes.

### What’s A Driver?

Before we get too deep, let’s make sure we’re all playing on the same field. *A driver* is a program that interacts directly with a hardware device or peripheral. Naturally, the driver program must have intimate knowledge of the hardware piece in question.

In the case of VGA graphics, the driver is what actually writes to the Digital-to-Analog Converter chip that sits on the graphics card.

### Driver

A driver, commonly known as a *device driver*, is a program that links a piece of hardware with an operating system. In other words, drivers bridge the gap between hardware and software.

SVGAlib contains several drivers for a multitude of cards. Although the library is much more than a simple collection of hardware interface programs, these drivers do comprise a very important and irreplaceable portion of the completed package.

As we proceed, it’s assumed you’ll be dealing with the following:

- A *Super VGA card*—That is, a card with extended memory and perhaps enhanced functionality, but one that’s also fully compatible with the VGA standard. Of all the cards available today (in the mass market), the vast majority should meet this requirement, with the possible exception of Permedia chipsets.
- A *PCI (or AGP) connected card*—It’s beneficial to have a modern bus such as these when detecting the card type, as well as finding the linear aperture.
- *Knowledge of the extended features of the chipset*—This knowledge can be obtained from the specifications released by the manufacturer (for example, in a spec book), or you can “borrow” it from the source code of another driver (such as an XFree86 driver for the same chipset). Hey, it’s what Open Source is all about.

### Other Files

To help get you started, it’s suggested that you also get the following:

- *vgadoc4b.zip* (or a later version)—This package includes valuable information regarding the standard VGA hardware registers as well as specifications pertaining to many common chipsets. A copy is included with this book’s companion CD-ROM.
- A *current release of SVGAlib*—It’s assumed that you’ll already have this, but if not, you can always get an update from the enclosed CD-ROM, or else from www.svgalib.org.
- *Xlikit.tgz*—If your card is supported by XFree86, you should get the *X Windows* link kit: Xlikit.tgz. Otherwise, if your card is supported by the *XFree86_SVGA* server, you should get the XFree source.

You can find the recommended X files (no pun intended) at the following URLs:

```
http://ftp.xfree86.org/pub/XFree86/current/binaries/Linux-i8x6-libe5/Xlikit.tgz
http://ftp.xfree86.org/pub/XFree86/current/source/X333serveronly.tgz
```

### Coding Your Driver

This section explains, step by step, how to put your driver together.

#### Step One

In the src subdirectory of your SVGAlib distribution, you'll find a source file called skeluton.c. This file is a generic, “bare-bones” driver template, and it's what you'll be working with to create your new driver. You won't want to mess up your pristine copy of skeluton.c, however, so don't work with it directly. Instead, copy skeluton.c to a new location and rename it. For example, you might use /usr/src/drivers/chipset.c, where chipset is the name of the chipset in question.

#### Step Two

Here comes the meat of the project. You'll now have to fill in the blanks. The functions that you'll need to customize are the following:

- `sk_setpage(int page)`
- `sk_saveregs(unsigned char regs[])`
- `sk_setregs(const unsigned char regs[], int mode)`
- `sk_initializemode(unsigned char *moderegs, ModeTiming *modetiming, ModeInfo *modeinfo, int mode)`
- `sk_unlock(void)`
- `sk_test(void)`
- `sk_setdisplaystart(int address)`
- `sk_setlogicalwidth(int width)`
- `sk_init(int force, int par1, int par2)`

Now it's time to shed some light on these internal functions. Matan Ziv-Av, author of the now-famous VESA driver for SVGAlib, has generously provided the bulk of the information given here. Thanks, Matan!

Matan's examples have been taken from the banshee.c driver, which was written according to the specifications available from 3dfx, and from the (hypothetical) millenniumll.c driver, written in accordance with the XFree86 source.

### Customizing sk_setpage()

This is a simple function. A mistake commonly seen here occurs when all your linear programs work correctly, but code that uses paged memory may have blocks (full width \* ??? lines) that are moved.

Listing 20.1 shows the hypothetical code for millenniumll.c (hypothetical, because X only uses linear mode and not paged memory), and Listing 20.2 details the corresponding code for banshee.c.
