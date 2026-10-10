# # Chapter 7
# Fonts

# ## Key Topics:

+   - Bitmapped and scalable fonts
+   - Integrating fonts into code
+   - How SVGAlib fonts are constructed
+   - FontBuilder.c
+   - FreeType

# ## What Is A Font?

Some might argue that fonts aren't really a part of graphics, but I disagree. Fonts appear on the screen, and they comprise a significant portion of graphical programs, so I feel their inclusion here is appropriate. In this chapter, I'll cover what fonts are and how they work with SVGAlib. You'll then learn how to utilize existing fonts and create your own, either by hand or with the assistance of a "font generation" program. Also, you'll see what work is being done to bring SVGAlib's fonts up to speed with those found in X Windows and other operating systems.

First of all, what is a font? A font can be defined as a collection of typewriter-rewritten characters, all with a consistent design or style. For example, the words in this book are written in Times New Roman, a standard word processing font. Thousands of other fonts (or typefaces) are available, and many can be found on the Web, free of charge. Others are created by professional designers and cost several hundred dollars each. Regardless of your preference, you can almost always find a font to fit your needs. What's more, there's virtually no limit to the number of possible fonts—you're only limited by your imagination in creating new and unusual character sets.

Fonts are stored in data files, which are then accessed by executables at runtime. The application reads the data contained in the font file and uses that information to produce, or render, the visible characters on your screen. Figure 7.1 shows two rendered SVGAlib fonts.