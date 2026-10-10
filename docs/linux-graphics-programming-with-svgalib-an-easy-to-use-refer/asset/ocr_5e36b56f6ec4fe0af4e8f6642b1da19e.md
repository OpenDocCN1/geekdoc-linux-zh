# Listing 20.1  Excerpt from milleniumll.c.

```
{
    outw(0x3de, (page<<8) | 4);
}
```

# Listing 20.2  Excerpt from banshee.c.

```
{
    page<<=1;

    outl(banshee_io_base+0x2c,
        ((inl(banshee_io_base+0x2c)&0xfff00000)|
         (page)|(page<<10)));
}
```

# Customizing *sk_savers*() And *sk_setregs*()

These functions should save and restore the original state of the SVGA card (generally speaking, this will be text mode) so that the card can be restored to a previous mode no matter what a program does (that is, no matter how badly it bombs). Your objective is to restore text mode properly.

Any registers changed by the driver should be saved, as well as registers that might be changed by other programs (X, SVGATextMode, and so on). Listing 20.3 details *banshee_saveregs*().

# Listing 20.3  The complete *banshee_saveregs*().

```
typedef struct {
    unsigned int pllCtrl0, pllCtrl1, dacMode, dacAddr,
                vidProcCfg, vidScreenSize, vgaInit0,
                vgaInit1, vidDesktopStartAddr,
                vidDesktopOverlayStride;
} *HWRecPtr;

static int banshee_saveregs(unsigned char regs[])
{
    HWRecPtr save;

    banshee_unlock();

    save=(HWRecPtr)(regs+62);

    regs[BANSHEEREG_SAVE(0)]=svgalib_inCR(0x1a);
    regs[BANSHEEREG_SAVE(1)]=__svgalib_inCR(0x1b);
    save->pllCtrl0=inl(banshee_io_base+0x40);
    save->pllCtrl1=inl(banshee_io_base+0x44);
    save->dacMode=inl(banshee_io_base+0x4c);
    save->dacAddr=inl(banshee_io_base+0x50);
```