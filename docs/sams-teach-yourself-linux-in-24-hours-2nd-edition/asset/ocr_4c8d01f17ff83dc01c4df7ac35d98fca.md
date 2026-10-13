# Converting and Viewing Graphics

There are a number of ways to convert graphic files to different formats using the programs installed on your system. Several of the painting or drawing programs discussed in this hour translate graphics, and many programs in Table 16.1 also work as filters in piped commands (see Hour 6, "Using the Shell," for details) to translate graphics.

You can use different combinations of these commands to convert files. OpenLinux users, such as graphics artists or system administrators, convert files for different reasons. Artists or casual users might want to import or export graphics for use by different drawing programs. System administrators might look for a side benefit of converting graphics to save disk space. In some instances, the savings can be considerable. Look at the following example:

```
# xwd >graphic.xwd
# xwdtopnm <graphic.xwd | convert - graphic.jpg
xwdtopnm: writing PPM file
# ls -l graphic.*
-rw-r--r-- 1 bball users 11003 Jan 27 14:21 graphic.jpg
-rw-r--r-- 1 bball users 851523 Jan 27 14:17 graphic.xwd
```

The first command line uses the xwd client to create an X11 window dump graphics file (.xwd) after you select a window and press your left mouse button. The window dump file is converted to .pnm format with the xwdtopnm command, and the output stream is fed into the convert command to create a .jpg graphics file. The hyphen (-) following the convert command specifies that the standard input should be used in lieu of an input filename. As you can see, the .jpg graphics file is more than 77 times smaller than the X11 window dump graphics file!

![](bbox=[0.1, 0.78, 0.2, 0.86])

> Results and benefits of file compression vary, depending on the size of the graphics file and compression settings. See the convert man page for details.

There are also many graphics programs not listed in Table 16.1 that can be used to alter graphics images. For example, the pnrotate, pnmsmooth, and pnmscale commands rotate, smooth, and resize graphics images. You can use a variety of these programs to not only convert graphics, but change their appearance or orientation.

If you’re using pipes to convert graphics, you also can change the images on-the-fly by applying these filter programs. For example, if you have a graphics file in .xpm format