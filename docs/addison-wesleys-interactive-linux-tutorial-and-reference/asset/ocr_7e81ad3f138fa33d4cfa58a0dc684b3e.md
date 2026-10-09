Note that, unlike **more**, when you reach the end of the file with  **less**, you do not return to the command prompt. This gives you the option to continue scrolling back through the file—an option that you do not have with **more**.

+   g.  Press the letter **q** to quit and return to the command prompt.
+         On most systems, you cannot use <Ctrl-C> to quit **less**.

As you saw in this module of the CBT course, **less** gives you many options for controlling the output.

**help** gives you a list of the various switches, or arguments, that you can use to modify the output of a command. Even when the output is lengthy, as it is with `ls --help`, the information that **help** provides is terse and usually limited to command syntax.

While **man** files are also terse, they nonetheless provide a great deal more information about the command. For example, you will find not only a list of switches but more detail about the effect of each switch. However, the **man** files are not intended to be instructional in the sense that the *Linux Made Easy* is instructional. A certain amount of knowledge about, and experience with, Linux is often assumed. Still, reading the **man** pages can often be illuminating.

+   5.  Read the **man** page about the command `mv`.
+       a.  Type `man mv`
+       b.  Press <Enter>

Your screen will look similar to Figure 7-2, which shows the first several lines of the output from `man mv`.

The **man** pages provide what is often referred to as "system documentation." How these pages are displayed, however, is determined by the system on which they are displayed, not by the **man** pages themselves. This means that the way in which you control the scrolling of the output will vary from one system to another. Many systems use the utility **less** to display the **man** pages.