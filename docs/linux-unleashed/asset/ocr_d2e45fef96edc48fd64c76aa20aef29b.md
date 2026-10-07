> **Note**

To simplify the directory structure for XFree86, links are usually created to a directory called `/usr/X11` which can be linked to `/usr/X386` and `/usr/X11R6`. Check your directory structure to determined which links are in place on your system. Also check your `PATH` environment variable to see which directory is in the search path (if one has been added at all).

# Choosing an X Server

Before installing XFree86, you must decide which type of server to use. The XFree86 servers are drivers for the video system (because X is a GUI, it makes extensive use of the video card in your system). Choosing the wrong type of server for your video card can cause your entire system to behave erratically (and in some cases damage your video card or monitor!). Be sure that the server matches your hardware.

There are several drivers available in most XFree86 distribution sets, and the names of the files tend to indicate the video card they are designed for. For example, you may encounter the following server files in most XFree86 versions:

+   - XF86_Mono: Monochrome video card (generic)
- XF86_VGA16: 16-color VGA video card (generic)
- XF86_SVGA: Color SVGA video card (generic)
- XF86_S3: Accelerated server for S3-based video cards
- XF86_Mach8: Accelerated server for Mach8 video cards
- XF86_Mach32: Accelerated server for Mach32 video cards
- XF86_8514: Accelerated server for 8514/A video cards

The generic indications in the preceding list mean that the server has no card-specific instructions, whereas the other servers have card-specific video card requirements. For example, the XF86_S3 server can be used only with video cards using the S3 chipset. Check with your video card documentation (or use a diagnostic utility program) to determine your video card’s chipset. Your distribution version of XFree86 probably has other specific server versions, so check the documentation for compatibility details.

The generic server drivers work with most cards that provide VGA and SVGA support. However, because the generic driver provides only the basic VGA and SVGA video instructions, any fancy features or extra power your video card may have will not be used. That’s why the card-specific servers were developed: They let you use the full capabilities of fancy video cards.