![](bbox=[0.35, 0.12, 0.65, 0.38])

Figure 8-6 xeyes follow your mouse, wherever it goes

# CUSTOMIZING X

# What are some of the things I can do to customize X Windows and what files do I need to change in order to do this?

Among other things, you can change the colors, fonts, appearance, and menus. There are two basic files that you have control of and they both reside in your $HOME directory—.Xdefaults and .mw mrc. The first controls the options and settings for the X server itself, while the second controls the behavior of the Motif Window Manager. You can also add other, task-specific files for a particular situation. And, finally, each application may have a special set of defaults that you can set. The default versions of these files, which should only be changed by your system administrator, are kept in the /usr/lib/X11/app-defaults directory. However, you can easily copy any of these files to your home directory to give you a baseline to work from. Some applications will read a "dotted" version of these files on start-up; others prefer that you include the settings in your .Xdefaults file. But in all cases, you can explicitly load these settings if you want. We strongly recommend that you do this when first making changes to a particular set of resources. Then and only then, if they really are what you want and expected, should you add them to the default files.