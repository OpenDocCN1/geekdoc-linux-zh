# 518 TOOLS AND UTILITIES

![](bbox=[0.319, 0.076, 0.863, 0.263])

Figure 15.9 The contents of a Photo CD.

# Other programs for image processing and graphics conversion

If you think the xv and ee image processing functions are not flexible enough, you should take a look at the gimp program. The program is extensively described in Chapter 20 from page 659 onward.

If, on the other hand, you are confronted with exotic graphics formats or if you want to convert a whole collection of files into another means of a script (without user interaction), there are other alternatives: the program package Image Magick provides both single commands and an interactive interface. For conversion, a proprietary intermediate format (MIFF) is used.

A similar approach is also followed by the NetPBM package (formerly Portable Bitmap Utilities). Here, the PBM format is used as an intermediate format. For, example, you have to convert hundreds of MS Windows bitmaps into PostScript format, these utilities are the right choice.

# 15.4 Displaying documents and graphics

# Displaying PostScript files (ghostview, kghostview, gv)

In principle, ghostview is nothing but a graphical user interface for the already introduced gs (GhostScript) program. ghostview can cope with both PostScript graphics and documents running to hundreds of pages. If the document corresponds to the PostScript standards, you can freely jump between page numbers. Otherwise, the file can only be read sequentially (that is, page after page without the possibility of skipping pages or leaving them back).

Depending on the distribution, ghostview is compiled with different widget libraries. This has the consequence that ghostview buttons and scroll bars look different than that shown in Figure 15.10. However, this difference only concerns the visual outcome; the function of the program remains the same.