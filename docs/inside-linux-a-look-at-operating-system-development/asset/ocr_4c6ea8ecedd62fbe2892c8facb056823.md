gwm called the EMACS of window managers because of its extensibility

But this list cannot be anywhere complete because almost all of these features can be reconfigured by changing the appropriate configuration file. These configuration files are often collections of triples: user action, context, and result. For instance, pressing the left mouse button when the pointer is on the title bar of a window causes that window to be raised to the top, or pressing the right mouse button while the control key is pressed with the pointer in an xterm window presents a font selection window. (In this latter case, the configuration is specific to the X terminal emulation, not a window manager.)

# 3.2.4 File Manager

One of the hottest GUI applications is the file manager. This program reduces the need for a command line interpreter because it allows one to start programs by clicking on an icon or dragging and dropping one file's icon onto another icon.

One tool distributed with Linux is xfm, a file manager which has been under development for over five years by Simon Marlow, Albert Graef and others. Graef writes:

> This is a powerful file and applications manager program written using the X toolkit. It contains virtually all of the features that you would expect in a file manager—move around your directory tree in multiple windows, and move, copy or delete files with simple mouse operations. Directory displays are updated automatically in regular intervals when the contents of a displayed directory changes. The integrated application manager allows you to load files into your favorite applications from the file manager by dragging icons. It can also be used as a “shelf” onto which you can place files and directories you are currently working with. A special LOAD action for application files enables you to manage different application groups.
> 
> User-definable file types allow you to specify a command to be executed when double-clicking on a file or dropping