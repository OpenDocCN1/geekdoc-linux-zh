*User HOWTO* and *The Configuration HOWTO* (for how to read them, see Recipe 2.8.6 [Reading System Documentation and Help Files], page 50).

# 4.7.1 Switching Between Video Modes

A *video mode* is a display resolution, given in pixels indicating the horizontal and vertical values, such as 640x480. An X server can switch between the video modes allowed by your hardware and set up by the administrator; it is not uncommon for a machine running X to offer several video modes, so that 640x480, 800x600, and 1024x768 display resolutions are possible.

To switch to another video mode, use the ⊕ and ⊖ keys on the numeric keypad with the left CTRL and ALT keys. The ⊕ key switches to the next mode with a lower resolution, and the ⊖ key switches to the next mode with a higher resolution.

⇒ Here are two ways to use this.

+   - To switch to the next-lowest video mode, type: CTRL-ALT-⊕
+   - To switch to the next-highest video mode, type: CTRL-ALT-⊖

To cycle through all available video modes, type either of these key combinations repeatedly.

**NOTES:** For more information on video modes, see *The XF86 Video Timings HOWTO* (see Recipe 2.8.6 [Reading System Documentation and Help Files], page 50).

# 4.7.2 Running X Clients Automatically

The `.xsession` file, a hidden file in your home directory, specifies the clients that are automatically run when your X session first starts ("hidden" files are explained in Chapter 5 [Files and Directories], page 125). It is just a shell script, usually containing a list of clients to run. You can edit your `.xsession` file in a text editor, and if this file doesn't exist, you can create it.

Clients start in the order in which they are listed, and the last line should specify the window manager to use. The following example `.xsession` file starts an `xterm` with a black background, white text, brown cursor, and no scrollbar, puts an `xclock` in the upper left-hand corner (AfterStep's clock inspired by the NEXTSTEP "tear-off" calendar clock), starts the Emacs text editor, opening the file "~/TODO" into a buffer of its own, and then starts the AfterStep window manager: