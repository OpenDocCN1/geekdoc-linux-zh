# Step One

In the src subdirectory of your SVGA1ib distribution, you'll find a source file called skeluton.c. This file is a generic, “bare-bones” driver template, and it's what you'll be working with to create your new driver. You won't want to mess up your pristine copy of skeluton.c, however, so don't work with it directly. Instead, copy skeluton.c to a new location and rename it. For example, you might use /usr/src/drivers/chipset.c, where chipset is the name of the chipset in question.

# Step Two

Here comes the meat of the project. You'll now have to fill in the blanks. The functions that you'll need to customize are the following:

+   - sk_setpage(int page)
+   - sk_saveregs(unsigned char regs[])
+   - sk_setregs(const unsigned char regs[], int mode)
+   - sk_initializemode(unsigned char \*moderegs, ModeTiming \*modetiming, ModeInfo \*modeinfo, int mode)
+   - sk_unlock(void)
+   - sk_test(void)
+   - sk_setdisplaystart(int address)
+   - sk_setlogicalwidth(int width)
+   - sk_init(int force, int par1, int par2)

Now it's time to shed some light on these internal functions. Matan Ziv-Av, author of the now-famous VESA driver for SVGA1ib, has generously provided the bulk of the information given here. Thanks, Matan!

Matan's examples have been taken from the banshee.c driver, which was written according to the specifications available from 3dfx, and from the (hypothetical) millenniumll.c driver, written in accordance with the XFree86 source.

# Customizing sk_setpage()

This is a simple function. A mistake commonly seen here occurs when all your linear programs work correctly, but code that uses paged memory may have blocks (full width \* ??? lines) that are moved.

Listing 20.1 shows the hypothetical code for millenniumll.c (hypothetical, because X only uses linear mode and not paged memory), and Listing 20.2 details the corresponding code for banshee.c.