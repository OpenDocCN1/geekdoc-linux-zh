
most cases, the easiest method is to first create the window and then create a GC for use in graphics requests for that window.

## COLORMAPS

One of the more difficult subjects to understand in X programming is the concept of a colormap. Actually, the concept itself is relatively easy to comprehend, but following the many rules for using colormaps can be an intricate and difficult process to learn. Because video hardware varies widely in the world of X programming for Linux and UNIX, a colormap might be a very different animal from one display to another. Chapter 28, “Breaking Out of Xlib Fundamentals,” explains how to use colormaps.

A colormap assumes only that the display is bitmapped—that is, each pixel (picture element) on a screen displays one distinct dot. The X server cannot work with other types of video hardware such as vector displays, but those are rarely used for computer terminals, anyway. Usually, virtual colormaps can be swapped with the hardware’s default colormap, and in that way, provide instant color configurations for multiple applications, or even for multiple windows within the same client. Depending on the number of available colors, however, this technique can cause color changes among inactive windows, especially when a color-intensive application receives the focus. For example, bringing up a true-color application such as a photographic editor might cause background windows to blush suddenly in shocking pink. Despite such quirks, however, colormaps do more than just provide a programming interface to video hardware. In most cases, they also permit clients to define the colors they need with no concern for how many or what types of colors are actually available.

A key element of a colormap is the concept of a *bit plane*. Typically, video display hardware provides memory that stores one or more bits per pixel. Each bit is a member of one bit plane for all of the display’s pixels. Although plenty of 8- and 16-bit-plane displays still are in use, 24-bit-plane color displays are fast becoming as common as toaster.

The number of bits in the video display’s circuitry determines the *depth* of the display and, indirectly, the number of possible colors it can display. Each pixel on a screen is associated with the bits in one or more planes. On a 24-bit-plane video system, each pixel is represented by a 24-bit integer, with one bit on each plane. Figure 26.2 shows conceptually how bit planes represent a pixel’s value in video memory.

![](img/6eab91cc30158075ed10d0cabbac9029_658_0.png)

**Figure 26.2**  
In many systems, one pixel value is represented as a number of bits, each a member of a bit plane.

## INTRODUCING XLIB PROGRAMMING

Monochrome displays differ in the way their color values are interpreted. Simple monochrome displays might even be one-dimensional, using a single bit (one plane) for each screen pixel. Such displays have only two colors, known in X programming as “white” and “black,” even though the actual colors can be any contrasting hues (green and light green, for example). More common, however, especially in desktop publishing applications, are monochrome grayscale graphical displays. In these types of displays, bit planes provide index values into a colormap’s grayscale intensity levels.

Regardless of the type of hardware on your system, it’s important to realize that bit-plane values in video memory do not directly represent colors. (However, some true-color displays might be an exception to that rule.) Instead, the bits in video memory are used in one way or another as indexes into arrays of other values such as red, green, and blue levels that determine the actual colors you see onscreen. This permits programs to work on a variety of hardware and also enables users and system administrators to fine-tune colormap values so that, for instance, bluely look blues blue.

Using colormaps may be difficult, but the end results are highly advantageous because they result in X client software that works correctly on all types of video hardware. You don’t have to understand exactly how bit-plane values are translated to actual color values or grayscale intensities. Ideally, even if the screen supports only one-dimensional black-and-white pixels, the user should be able to see all the application’s output.

That’s enough background. Now, let’s take a look at programming an X client and the basic steps needed to get a window to appear onscreen. Because even that simple task takes many lines of code, the following sample program, xwelcome.cpp, is discussed in pieces here. For reference, the complete listing follows at the end of the section. Also see the sidebar, “Compiling X Clients,” for how to compile and run the xwelcome.cpp program and other X client applications listed in this and the next two chapters.

In most cases, about six basic steps are involved in a typical X client application. The following sections describe each of these steps in reference to the xwindow.cpp listing on the CD-ROM (in the c26/xwelcome path).

### Compiling X Clients

Because compiling X applications requires several compiler and linker options, it’s impractical to type the necessary commands. For this reason, each example program in this and the following chapters is stored in a named directory such as src/c26/xwelcome. In each named directory is a file named Makefile that specifies the

> Note
> 
> Tricks with video bit planes can produce interesting graphical illusions. For example, by drawing into one or more planes, images appear to float on top (or within) other images without affecting the bits in other planes.
