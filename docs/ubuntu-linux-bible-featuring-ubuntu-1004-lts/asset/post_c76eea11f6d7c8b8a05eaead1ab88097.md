
# What Is Compositing? Why All the Fuss

Most current graphics cards provide at least 128 MB of onboard video RAM, while most of the video controllers integrated into today's motherboards enable you to allocate at least a similar amount of system memory to the graphics controller. Having a significant amount of memory available allows the video cards themselves to do substantial onboard graphics processing. Not only today's video cards provide high-performance, built-in graphics processors, but offloading graphics calculations from the CPU and window manager to the video card improves overall performance and responsiveness.

As discussed in Chapter 5, "Using the GNOME Desktop," Linux systems use the Window System (also known as XI or simply X) as the graphical framework that underlies most Linux desktop environments and window managers. A window manager handles creating, moving and managing windows on high-resolution monitors that are managed by an X Server, and they can be either stand-alone or components of a desktop environment that provides higher-level capabilities such as drag-and-drop. The X Window System uses high resolution monitors as a bitmap display, which means every bit (pixel) on the screen is actually mapped to a memory location. This enables fast graphics operations to be done by manipulating memory, and the result of that is immediately displayed on your monitor.

The term compositing refers to the combination of graphical or visual elements from separate sources into single images. In Linux systems, a compositing manager is an X Window System client that redraws windows and other parts of the bitmap display to video memory, tracks changes to that off-screen memory, and handles merging the updated images into the system's bitmap display when changes occur and the screen has to be redrawn. An X Window System compositing window manager is therefore a unified window manager and compositing system that performs conventional window management functions while integrating and displaying high-quality, high-performance graphics being created and managed in your system's video memory, including special effects such as transparency and translucency. Traditional window managers (as discussed in the "Using a Window Manager" at the end of Chapter 5) are referred to as tiling or stacking managers—tiling window managers display side-by-side with no overlap, while stacking window managers display windows on top of overlapping one another, with no transparency. Compositing adds transparency and translucency to the standard stacking window manager model by taking advantage of modern graphics.

## Tip

Although the terms transparency and translucency are often used interchangeably, they actually have different meanings for truly hardcore graphics fans. A transparent physical material shows objects that are behind it and does not reflect light off its surface. A translucent physical material reflects some of the light that hits it. See the OpenGL FAQ (www.opengl.org/resources/faq/technical/transparency.html) for a more verbose explanation.

## Chapter 6: Using the Compiz Window Manager

Modern underlying window managers like Compiz use separate applications to handle window decorations (window borders, buttons, frames, etc.), while the window manager focuses on window placement, movement, and special effects. This provides a flexible environment that follows the traditional UNIX philosophy of writing smaller applications that do one thing, do it well, and can work together to perform complex tasks.

Compiz, which is all the rage in Linux circles nowadays, provides a nice blend of the best possible use of high-performance graphics hardware, providing attractive window effects for fans of eye candy and a flexible window management environment that is easily modified and extended.

## Compiz History: Compiz, Emerald, Beryl, and Friends

This section discusses the history of composing window managers on Linux and the window managers that led to Compiz and Compiz Fusion. Not everyone wants a history lesson, so if you're not interested, feel free to skip ahead. This section will provide a handy reference after you've heard terms such as Beryl, Emerald, Compiz, and Compiz Fusion over and over what they mean.

Like all graphics components on Linux systems, compositing window managers depend on the capabilities of the underlying X Window System. To provide high-performance special effects, compositing window managers require especially tight integration between graphics and the window manager. Compiz is not the first compositing window manager—compositing has been supported for a while in window managers as Metacity, the window manager that was traditionally associated with GNOME 2.2 (and on Ubuntu releases prior to 7.10), and Xfwm, the window manager introduced by the Xfce desktop (http://xfce.org).

## Tip

If you find that Compiz is too resource-intensive for your tastes, or if you simply want to run another window manager, you may want to experiment with running the Xcompmgr composition manager with that window manager. Xcompmgr is designed to provide the graphical eye candy with that window manager. If you like it, install xcompmgr, switch to your favorite window manager, as explained in Chapter 5 entitled "Using a Window Manager."

Regardless of the fact that Metacity, Xfwm, and other window managers pioneered compositing, Compiz was the first widely-known window manager that was designed from the ground up to support compositing via OpenGL.

## Part II: Ubuntu for Desktop Users

One of the reasons behind the foundation of AGL was that some people felt that much of the development of Xgl was local to Novel and didn't invite enough community discussion. Similarly, the Beryl project emerged as a fork of Compiz when people felt that the development of Compiz was moving too slowly.

As mentioned in the previous section, one of the core ideas of Compiz is to use separate applications to handle window decorations. Compiz provides the gtk-window-decorator to customize window decorations in the GNOME environment, which can even use Metacity themes. Beryl's primary window decorator is Emerald, although decorators named Helior and Aquamarine were available at one time.

Beryl racked a tumultuous set of plug-ins and whizzy features, while Compiz moved to AGL and became more open. Eventually, the people working on the Beryl project merged with the folks who were developing Compiz, resulting in the Compiz Fusion project. The goal of this project is to improve the usability and functionality of Compiz by porting most of the whizzy things that were done for Beryl to Compiz, and to continue to develop additional libraries, plug-ins, and those that make Compiz both a fun and functional graphical environment. The Compiz Fusion folks have even ported Emerald to work with Compiz, to ensure that you will always have an impressive (and sometimes-bewildering) smorgas of graphical choices. Today's Compiz comes with a core set of

- X Window servers such as ATI, Intel, and NVIDIA, providing impressive performance
- X servers such as the standard X.Org server (as of release 7.1) use AGL

## Tip

I've found that some systems with ATI or NVIDIA chips work better with AGL than the standard X server. This is especially for laptop computers, which often use ATI or NVIDIA chips that require proprietary or specialized drivers. If you have problems getting Compiz working with the standard X server, it's worth trying AGL.

Compiz was designed to provide a flexible window management framework to which plug-ins can easily be added without the need to reinstall the entire window manager. Thanks to AGL and lots of work done, Compiz now works with the standard X.Org server, and AGL development has been merged directly into X.Org.
