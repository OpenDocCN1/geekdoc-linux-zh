```
```text
libc.so.5 -> /lib/libc.so.5 (0x40060000)
libm.so.5 -> /lib/libm.so.5 (0x401c0000)
```
```

From this output, you can infer that **fun** (one of the SVGAlib demo programs) requires four external libraries. Sometimes, though, you’ll see the following:

```
```text
statically linked (ELF)
```
```

This, of course, means that the program is statically linked and doesn’t depend on any external files.

# ## The Vgagl Library

There’s one more shared and/or static library that you’ll get with any SVGAlib installation—vgagl. This is a higher-level library that allows you to perform more advanced functions, such as drawing shapes with a single command. It also allows the use of a *framebuffer*, which is like an invisible screen. The idea is this: You draw to the invisible screen and then transfer your drawing to the visible (real) screen in one fell swoop, thus eliminating the annoyance of screen flicker. It has other uses as well, which I’ll discuss when we get into coding.

Hopefully, these sections have made it easy for you to understand how SVGAlib connects to your programs. When you build a program with SVGAlib, you link to it, just like you link to libc.so.5 or glib.

# ## Different Libraries That Produce Graphics

SVGAlib isn’t the only graphical library, but, in my mind, it’s the best. Other libraries, such as consoles, allow you to move your cursor around the screen and change your colors, but I don’t consider that to be true graphical output. Aaalib lets you turn graphic files into ASCII art, but again, it’s still displayed as text. The only serious contender to SVGAlib is X Windows.

# ### Differences Between SVGAlib And The X Windowing System

Readers of this book may already be familiar with XFree86, otherwise known as the *X Windowing System*. But how are X and SVGAlib different, you might ask? They both run on Linux, and they’re both used to display graphics.

The key difference is that XFree86 is a *server application* (or a *daemon*), such as syslogd and named (and all the other programs that end with d and pop up when you boot up your system). Unlike SVGAlib, the X server must be running in the background to process requests. This means that you can’t call XFree86 from a shell script; it has to be started first. Generally, if you plan on using XFree86 applications, you’ll need to have your X server running at all times.