

# Linux 应用程序中的共享库 761

以下是 `ldd` 对一个典型 C 程序的报告：

```
libc.so.6 => /lib/libc.so.6 (0x00b0a000)
lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x00af1000)
```

复杂的程序，例如 GIMP（类似于 Adobe Photoshop 的程序），使用了许多共享库。要查看其共享库需求，请输入以下命令：

```
ldd /usr/bin/gimp
```

这是在我 Fedora 核心版上显示的列表：

```
libmgwidgets-1.3.so.26 => /usr/lib/libmgwidgets-1.3.so.26 (0x03783000)
libmgcolor-1.3.so.26 => /usr/lib/libmgcolor-1.3.so.26 (0x00e0000)
libmgmodule-1.3.so.26 => /usr/lib/libmgmodule-1.3.so.26 (0x00d6000)
libmgbase-1.3.so.26 => /usr/lib/libmgbase-1.3.so.26 (0x001a1000)
libmgthump-1.3.so.26 => /usr/lib/libmgthump-1.3.so.26 (0x00de8e0)
libmgmath-1.3.so.26 => /usr/lib/libmgmath-1.3.so.26 (0x00487000)
libmgpix-1.3.so.26 => /usr/lib/libmgpix-1.3.so.26 (0x0044b000)
libdk-x11-2.so.0 => /usr/lib/libdk-x11-2.so.0 (0x00762000)
libhibat-1.0.so.0 => /usr/lib/libhibat-1.0.so.0 (0x0011b000)
libpixbuf-2.0.so.0 => /usr/lib/libpixbuf-2.0.so.0 (0x00d35f00)
lib.so.6 => /lib/libm.so.6 (0x00dc4600)
libcursort-1.0.so.0 => /usr/lib/libcursort-1.0.so.0 (0x001b9100)
libpgaft-1.0.so.0 => /usr/lib/libpgaft-1.0.so.0 (0x0075b000)
libpang-1.0.so.0 => /usr/lib/libpang-1.0.so.0 (0x00731000)
libintl_lgpl_2.so.2 => /usr/lib/libintl_lgpl_2.so.2 (0x0032c000)
libpang2-1.0.so.0 => /usr/lib/libpang2-1.0.so.0 (0x003e0000)
libgobject-2.0.so.0 => /usr/lib/libgobject-2.0.so.0 (0x002a0000)
libmodule-2.0.so.0 => /usr/lib/libmodule-2.0.so.0 (0x007e0000)
libgio-2.0.so.0 => /usr/lib/libgio-2.0.so.0 (0x0015f000)
libglib-2.0.so.0 => /usr/lib/libglib-2.0.so.0 (0x001f5000)
libconfig-1.0.so => /usr/lib/libconfig-1.0.so (0x00168000)
libcreetype-6.so.0 => /usr/lib/libcreetype-6.so.0 (0x00101000)
libz-1.so.1 => /usr/lib/libz-1.so.1 (0x00d61000)
libthread-1.so.0 => /lib/libthread-1.so.0 (0x00d74000)
libm.so.6 => /lib/libm.so.6 (0x00aaa0000)
libx11.so.6 => /usr/lib/libx11.so.6 (0x00c71000)
librandr-2.so.0 => /usr/lib/librandr-2.so.0 (0x00199000)
libf6.so.6 => /usr/lib/libf6.so.6 (0x00d51000)
libxft.so.2 => /usr/lib/libxft.so.2 (0x00dc000)
```

（注：由于提供的待翻译文本似乎在某处发生了中断，且包含了大量重复的占位符逻辑，以下翻译基于您提供的文本结构进行针对性处理。）

## 动态加载共享库

在程序中动态加载共享库并使用该共享库中的函数是简单的。在本节中，我将演示如何执行此操作。头文件 `<dlfcn.h>`（那是 Linux 中的一个标准头文件）声明了加载和使用共享库的函数。

