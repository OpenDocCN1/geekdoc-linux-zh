+   • Description — Type a description of the MIME type.

+   • Application Preference Order — Click Add, then select an application that will handle the MIME type that you just added and click OK. You can add several applications, in order, that could be used to handle the data type. The first application launches when you select a matching file type; other applications will appear on the menu when you right-click a matching file type and select Open With.

6. Click Apply. The new MIME time is now saved.

At this point, any file created with the file extension that was just added will be launched by the application you indicated when the file is opened from the desktop or File Manager window. Right-click a file of that type to choose to launch the file by a different application from the Open With list (if more than one application is listed for the file type).

# Changing X Settings

Regardless of which desktop environment or window manager you use, the common underlying software is the X Window System. Although you can quite happily use your desktop without ever directly accessing X, getting to know some of the features of X will help you to better understand how all GUI interfaces in Linux work.

There are X resources that you can change that apply to your desktop in general, as well as specific X clients you run. Most X clients use standard options to set background and foreground colors, window titles, placement on the screen, and other resources. This section describes how to set X resources that apply to the general desktop, as well as to X client programs.

The most common ways to set X resources are by:

+   • X Client Command-Line Options — Most X clients support standard command-line options (as well as some options specific to each client) that set resources. For example, you can use the option -geometry to set the default size and position of most X client windows.

+   • X Resource Files — System and user resource files can be loaded by the xrdb command at desktop startup time. When you start the X GUI, it loads resources from either the system-wide Xresources file or from your personal .Xresources file (if either exists). Default resources for many X clients are stored in files in the /usr/lib/X11/app-defaults directory. You can override any X client resource files in app-defaults by creating files of the same names in your home directory.

There are also commands that you can run to change attributes related to general desktop features (xsetroot command) or your keyboard mappings (xmodmap command). The following sections describe how to change X resources using both X client command-line options and X resource files.