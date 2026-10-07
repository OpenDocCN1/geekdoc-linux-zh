
# GIMP Resources on the Web

There are many wonderful GIMP resources available for you on the Web. This is just a small list of sites. Try a search engine to find more.

The companion site for this book: http://www.peachpit.com/vqs/gimp/

The official GIMP site: http://www.gimp.org

GIMP news: http://www.xach.com/gimp/news

WilberWorks distributes and offers support for the GIMP: http://www.wilberworks.com

The GIMP 16 project, extending the GIMP for film production: http://www.film.gimp.org

# Compiling the GIMP

If you want to install the development version of the GIMP (see the sidebar below), or use a peripheral device driver (page 2), you will need to compile a new version of the GIMP. If you are a Linux/Unix programmer with experience in compiling programs, you won't find this difficult. If you don't have this kind of technical background, this can still be done (I did), you may find yourself using online resources and discussion groups to get past the tricky spots.

Generally, the process of compiling the GIMP starts with downloading the GIMP source code. You will need to have the GNU C Compiler (gcc) loaded on your system. In addition, there are some code libraries that also need to be present on your computer.

Compiling the GIMP is beyond the scope of this book, but if you're interested in doing so, you can go to http://www.gimp.org/INSTALL for detailed instructions.

# The Next New New Version of the GIMP

I wrote this book using RedHat Linux 6 and Version 1.0.4 of the GIMP. However, new versions of the GIMP are always being created. If you discover that the GIMP (as many folks do!) and want to be on the cutting edge of everything thing, you can download the latest Development Version of the GIMP at http://www.gimp.org/devel_ver.html. Be warned that the Development Version is uncompiled source code that needs to be compiled into a program. If you are an experienced programmer, this shouldn't be a problem, but for mere users, compilation of a new GIMP version will likely be difficult. And once the program is running, it is not guaranteed to be free of bugs.

![](img/5164bc49fb24f10213e18cc994b7b40c_18_0.png)

# Chapter 1

## The GIMP Screen (Figure 1)

1 The GIMP Toolbox 2a Current open image 2b Color mode 3 Image window

![](img/5164bc49fb24f10213e18cc994b7b40c_19_0.png)

THE GIMP SCREEN

## Key to the GIMP Screen

### 1 The GIMP Toolbox
The GIMP Toolbox is your gateway to creating amazing images. The Toolbox contains twenty-one-tools that perform various functions from selecting and painting to erasing and blurring.

### 3 Image window
The image window is the area on the screen where images are created. You can have as many image windows open at one time you want.

### 2A-B Titlebar
The Titlebar displays the currently open image name and the color mode in which the image is set.

### 4 Rulers
The mouse pointer's current position is indicated with marks on the vertical and horizontal rulers. The measurement unit they display is fixed at pixels.

# The Basics

### 5 Image display area
The image display area or canvas is the image window where graphics appear. It is bounded by a dashed line.

### 7 Pop-up menu
The pop-menu contains the myriad commands, filters, etc., used to manipulate an object. The popup menu is accessed by positioning the mouse pointer over the image window and clicking the right mouse button.

### 6 Guides
Guides are non-printing lines that come in two flavors—vertical and horizontal. Guides are used for aligning selections or layers, or for exactly delineating an area to be selected.

### 8 Special GIMP dialog boxes
There are seven dialog boxes that give access to essential items such as brushes, color palettes, layers, and tool options.

# Changing Keystroke Combinations on the Fly

The GIMP comes predefined with many keystroke combinations (also called hotkeys), such as Ctrl+N to start a new graphic and Ctrl+S to save a graphic. If you are used to working with other image manipulation programs and want to use the keystroke combinations you are familiar with, you can change the GIMP combinations on the fly. Here's how:

- 1. Use the mouse pointer to highlight the menu item you want change. For instance, you could right-click on the image window and highlight Image→Grayscale on the pop-up menu.

- 2. With the menu item highlighted, press the new keystroke combination on the keyboard you wish to use for that menu item, for example Ctrl+G. The keystroke combination will be reassigned to that menu item. The next time you want to access the menu item, just press your custom keystroke.

| File | Colors |
|---|---|
| Edit | Channel Ops |
| Select | Alpha |
| View | Print |
| Image | Grayscale |
| Layers | Indexed |
| Tools | Resize |
| Filters | Scale |
| Script-Fu | |
| Dialogs | Histogram |
| Transforms | |

# Tips

- Be aware that changing a keystroke combination for one item can affect another. For instance, in the example above, Ctrl+G is assigned to the Image→Grayscale command. By default, Ctrl+G opens the Gradient Editor. Changing this means Ctrl+G will no longer open the Gradient Editor.

- This book uses the preset GIMP keystroke combinations. If you create your own, they won't make the directions.

- If you want to reset the keystroke combinations to the preset default, open a Terminal window and use rm .gimp/menur at the command prompt. To find out how to open a Terminal window, take a look at on page 23.

# Chapter 1

## The GIMP Toolbox (Figure 2)

The GIMP Toolbox is the first (and only) thing you'll see when you launch the GIMP. (To create or open an image, use the File menu in the GIMP Toolbox.) The 21 tools in the Toolbox are used to manipulate a graphic in various ways. If you use other graphics programs, the Toolbox works just as you would expect: click the tool button to select the tool. To access the options for a tool, double-click on the tool button.

![](img/5164bc49fb24f10213e18cc994b7b40c_21_0.png)

# The GIMP Toolbox Menus

There are two menus available in the GIMP Toolbox (Figures 3–4). These menus give access to general commands, such as starting a new graphic, setting preferences, or creating new images using script-fus.

| File | |
|---|---|
| New | Ctl+N |
| Open | Ctl+O |
| About... | |
| Preferences... | |
| Tip of the day | |
| Dialogs | |
| Quit | Ctl+Q |

**Figure 3.** The File menu is used to create and open images, and exit the GIMP. It is also used to set preferences, the Tip of the day, learn about the creators of the GIMP, and the special GIMP dialogs.

**Figure 4.** The Xns menu is used to open the DB Browser, create screen shots, access script-fus, and view GIMP-related Web sites using a browser. Typically, the script-fus located on the Xns menu create new images in a new window.

# Script-fus and Plug-ins

Script-fus and plug-ins are two very powerful programming features that add functionality to the GIMP.

Plug-ins are little programs that let the user add extra features to the GIMP. In fact, much of the GIMP, except for core features, plug-ins have been integrated into the GIMP program. Since the GIMP is a modular program, it's easy to enhance the GIMP directly through the use of plug-ins without having to recompile or reinstall the entire program. Typically, plug-ins are coded in C. If you have some experience with C and want to create your plug-ins, visit http://gimp-plug-ins.sourceforge.net/doc/writing/html/plugin-in.html for directions.

Script-fus are essentially the macros of the GIMP. If you are familiar with macros (or scripting languages) from word processing programs, you know that a macro will vary various actions or repetitive tasks. Script-fus are usually written using a programming language called SCHEME. Go to http://xcf.berkeley.edu/~gimp-script-fu/script-fu.html to find out more about script-fus and how they are created.

To find out how to use the script-fus and plug-ins that come with the GIMP, turn to Chapter 16, Plug-ins and Script-fus, starting on page 247.
