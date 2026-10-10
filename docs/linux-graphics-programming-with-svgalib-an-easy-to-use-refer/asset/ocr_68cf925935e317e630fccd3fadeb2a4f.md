# Conclusion

SVGAlib fonts may appear frightening at first, but they're really quite simple once you get the hang of them. Of course, some of your fear might derive from the poor quality of the available bitmapmapped characters, many of which are truly scary. However, there are some nice fonts out there. Screen characters are useful in games and in many other programs, and it behoooves you to know how to use them.

As is the case with your other SVGAlib programs and utilities, if you've developed a nice SVGAlib font, feel free to submit it to www.svgalib.org for worldwide distribution. Don't worry, we'll give you credit.

With any luck, the FreeType library will one day be integrated with SVGAlib proper. Until then, we have Matan Ziv-Av to thank for making those functions available.

# Summary Of Functions Introduced In This Chapter

Here is a summary of the functions covered in this chapter:

+   • void gl\_expandfont(int fw, int fh, int c, void \*sfp, void \*dfp)
+   • extern unsigned char \*gl\_font8x8
+   • void gl\_setfont(int fw, int fh, void \*fp)
+   • void gl\_write(int x, int y, char \*s)
+   • void gl\_written(int x, int y, int n, char \*s)