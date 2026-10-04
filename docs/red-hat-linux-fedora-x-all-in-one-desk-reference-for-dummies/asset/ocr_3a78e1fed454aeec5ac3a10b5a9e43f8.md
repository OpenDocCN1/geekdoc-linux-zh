# Shared Libraries in Linux Applications 761

Here is what ldd reports for a typical C program:

```
libc.so.6 => /lib/libc.so.6 (0x00b0a000)
lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x00af1000)
```

A complex program, like the GIMP (Adobe Photoshop-like program) uses many shared libraries. To view its shared library needs, type the following command:

```
ldd /usr/bin/gimp
```

Here's the list displayed on my Fedora core:

```
libmgwidgets-1.3.so.26 => /usr/lib/libmgwidgets-1.3.so.26 (0x03783000)
libmgcolor-1.3.so.26 => /usr/lib/libmgcolor-1.3.so.26 (0x00e0000)
libmgmodule-1.3.so.26 => /usr/lib/libmgmodule-1.3.so.26 (0x00d6000)
libmgbase-1.3.so.26 => /usr/lib/libmgbase-1.3.so.26 (0x001a1000)
libmgthump-1.3.so.26 => /usr/lib/libmgthump-1.3.so.26 (0x00de8e0)
libmgmath-1.3.so.26 => /usr/lib/libmgmath-1.3.so.26 (0x00487000)
libmgpix-1.3.so.26 => /usr/lib/libmgpix-1.3.so.26 (0x0044b000)
libdk-x11-2.so.0 => /usr/lib/libdk-x11-2.so.0 (0x00762000)
lhibat-1.0.so.0 => /usr/lib/lhibat-1.0.so.0 (0x0011b000)
gibpixbuf-2.0.so.0 => /usr/lib/libpixbuf-2.0.so.0 (0x00d35f00)
lib.so.6 => /lib/libm.so.6 (0x00dc4600)
libcursort-1.0.so.0 => /usr/lib/libcursort-1.0.so.0 (0x001b9100)
libpgaft-1.0.so.0 => /usr/lib/libpgaft-1.0.so.0 (0x0075b000)
libpang-1.0.so.0 => /usr/lib/libpang-1.0.so.0 (0x00731000)
libintl_lgpl_2.so.2 => /usr/lib/libintl_lgpl_2.so.2 (0x0032c000)
libpang2-1.0.so.0 => /usr/lib/libpang2-1.0.so.0 (0x003e0000)
libgobject-2.0.so.0 => /usr/lib/libgobject-2.0.so.0 (0x002a0000)
libmodule-2.0.so.0 => /usr/lib/libmodule-2.0.so.0 (0x007e0000)
libgio-2.0.so.0 => /usr/lib/libgio-2.0.so.0 (0x0015f000)
lglib-2.0.so.0 => /usr/lib/libglib-2.0.so.0 (0x001f5000)
libconfig-1.0.so => /usr/lib/libconfig-1.0.so (0x00168000)
libcreetype-6.so.0 => /usr/lib/libcreetype-6.so.0 (0x00101000)
libz-1.so.1 => /usr/lib/libz-1.so.1 (0x00d61000)
libthread-1.so.0 => /lib/libthread-1.so.0 (0x00d74000)
libm.so.6 => /lib/libm.so.6 (0x00aaa0000)
libx11.so.6 => /usr/lib/libx11.so.6 (0x00c71000)
librandr-2.so.0 => /usr/lib/librandr-2.so.0 (0x00199000)
libf6.so.6 => /usr/lib/libf6.so.6 (0x00d51000)
libxft.so.2 => /usr/lib/libxft.so.2 (0x00dc0000)
libxender-1.so.1 => /usr/lib/libxender-1.so.1 (0x00f4f000)
liblinux-so.6 => /lib/liblinux-so.6 (0x0024f000)
libexpat-so.0 => /usr/lib/libexpat-so.0 (0x00da9a00)
```

In this case, the program uses quite a few shared libraries, including the X11 library (libX11.so.6), the GIMP toolkit (libgtk-x11-2.0.so.0), the General Drawing Kit (GDK) library (libgdk-x11-2.0.so.0), the Math library (libm.so.6), and the C library (libc.so.6).

Almost any Linux application requires shared libraries to run: