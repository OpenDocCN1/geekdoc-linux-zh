# 8 Chapter 1

```
"""will crash hard as soon as the program tries to enter
# linear mode.
# Enable this only if the resulting libraries will only be
# used on new kernels.
#
# NOTE: I found it very slow on occasion. There are several cases not handled
# optimally. (Like checking for console changes even when the hardware is not
# accessed at all). You might really consider disabling it. (MW)
# BACKGROUND = y"""
```

Background mode is disabled by default.

```
ONE_MAP = y
```

The linear video memory is normally mapped every time a new video mode is set to linear addressing. If **ONE_MAP** is enabled, the video memory will be mapped only once. This has the advantage that when modes are changed often, the system will not run out of memory space. This feature has been tested extensively with the ET6000 video card, but it should work for all other cards as well.

*Report any problems with it to Don Sccreat at secret@uiuc.edu.*

```
# INSTALLSTATICLIB = installstaticlib
```

Uncomment this line if you want to compile and install the static libraries. I’d suggest that you do so, but it’s not the end of the world if you don’t. To compile the static library later, just go to the source directory and type **make static**.

```
INSTALLSHAREDLIB = installsharedlib
```

And comment out this line if you don’t want to install the *shared libraries*. If you don’t install the shared or the static libraries, use **make static** first to enforce the building of just the static library; then the demos will use this local static library. Think twice before changing this one, though. Shared libraries are the foundation of **SVGAlib**. If this means absolutely nothing to you, take a break and jump ahead to the “SVGAlib Basics” section.

```
"""INSTALLLAOUTLIB = installlaoutcompat
#-------------------------------------------------------#"""
```

If your **TARGET_FORMAT** is ELF and a precompiled shared library a.out image is available, install the image in the first directory (named something like *aout/*) in **/etc/ld.so.conf**. If you want this, leave the above line alone.

```
KEEPSHAREDLIBS = keep
```