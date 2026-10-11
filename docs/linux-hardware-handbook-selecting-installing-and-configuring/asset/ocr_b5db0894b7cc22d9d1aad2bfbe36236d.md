One of the trickiest products to purchase, from a Linux point of view, is a video card (a k a a *video board*). The video card marketplace changes rapidly, driven largely by increasing demand for complex graphics in Windows games. Most of these games aren't available in Linux, however, so Linux's needs are more modest. What's worse, the developers of XFree86, the GUI system most often used in Linux, have a hard time keeping up with the ever-changing video hardware market. As a general rule, therefore, Linux support for video cards lags a few months behind the state of the art.

This isn't to say that it's *difficult* to find a video card that's suitable for use in Linux. The prob- lem is twofold, really:

+   * Without adequate research, it's easy to pick up a video card for which no XFree86 sup- port exists. The odds are in your favor even if you randomly select a product from the store shelves, but less so than for most other products.

+   * If you've narrowed your choice to a few specific products based on non-Linux criteria, it can be difficult to track down which cards are well supported in Linux. Many manufac- turers obscure important information, such as the chipsets they use, and it's not always obvious from the XFree86 documentation which specific products work and which don't.

This chapter exists to help you get around these problems.

# # Board Buses

One of the basic characteristics of a video card is the motherboard bus it uses. Video cards have been designed for just about every bus used on x86 computers. Most of today's cards use the AGP bus, although a few PCI bus cards are still available.

# ## ISA Bus

ISA bus video cards were common on 80386 and early 80486 computers, but have become quite rare since then. The reason is simple: The ISA bus lacks the capacity for high-speed transfers that are needed by modern video displays. The ISA bus is capable of a theoretical maximum transfer rate of 8MB/s. A 1024x768 display rendered at 16 bits (65,536 colors) holds 1.5MB of data, meaning that such a display can handle a maximum of only 5.3 updates per second. Although this is adequate for updating text in a word processor's window, it's not adequate for complex games, whose displays frequently change substantially in a fraction of a second.

Because most ISA video card designs are so old, most are well supported in XFree86. Therefore, if you have an old 80386 or 80486 computer on which you want to run Linux, chances are you'll have no problems with the video card. In a pinch, you should also be able to use a video card scavenged from such a computer on a more sophisticated machine.