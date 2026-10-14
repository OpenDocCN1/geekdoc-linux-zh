Regardless of the amount of video memory available and the number of possible planes, we can break down all types of screens into one of three basic categories:

+   - Monochrome single-plane systems
+   - Monochrome grayscale systems
+   - Color systems

For the purposes of programming X color graphics, it is usually only necessary to determine which of these categories best describes your system. In the first case, the client can use black and white for all its colors. However, if the client needs more than two colors, it has no choice but to display an error message and exit. In the second case, the client application can allocate grayscale color values in place of its usual colors. In the third case, the program can use color values provided in an X server database.

> Note
> 
> Various techniques are possible for investigating the type of video system available, but in most cases, it is best simply to give users the capability to choose their own color values, perhaps using command-line options or from a setup file. Color graphics programming in X involves an amount of guesswork, and it is probably not possible to write software that works exactly the same on all possible types of hardware running UNIX and Linux.

# THE X COLOR DATABASE

In most cases, by using a standard color name, your program has the best chance of producing predictable color graphics. Colors are defined in a database stored in file rgb.txt. This file contains a set of color names and associated RGB values known to the X server. Also in this file are grayscale levels symbolically represented as gray0 through gray100 (or grey0 through grey100) in single-integer steps. You may use these "colors" on color or monochrome grayscale systems. Table 28.1 shows some of the colors from the rgb.txt database in their declared order. Many colors have synonyms—for example, hot pink and HotPink are the same color. Some authorities indicate this file is stored in the path /usr/X11R6/lib/X11, but on my system, I found it in /usr/X11R6/lib/X11, so you might have to hunt for it. The X server uses a compiled version of this file—it doesn't actually read the text.

TABLE 28.1 SELECTED X COLOR NAMES FROM RGB.TXT

| snow | DarkSlateGrey | LightCoral |
| ghost white | dim gray | tomato |
| GhostWhite | DimGray | orange red |
| white smoke | navy blue | OrangeRed |
| WhiteSmoke | NavyBlue | red |
| antique white | cornflower blue | hot pink |
| AntiqueWhite | CornflowerBlue | HotPink |