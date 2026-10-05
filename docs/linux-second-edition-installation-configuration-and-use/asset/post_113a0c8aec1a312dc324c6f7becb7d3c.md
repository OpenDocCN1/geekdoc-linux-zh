
## MOUSE AND KEYBOARD UNDER X 247

### Mouse setting in XF86Config, if rpm -R is used as mouse server
```config
Section "Pointer"
Protocol "MouseSystems"
Device "dev/gpmdata"
EndSection
```

While gpm can mean the solution to many mouse dilemma, there are other mice where gpm and X do not agree. In this case, gpm must be halted with gpm -k before X is started. The gpm -k instruction can, for example, be included in xinitrc.

## Using the mouse

### Copying and pasting text with the mouse

In practically all X programs, you can use the mouse to copy sections of text and subsequently paste them into another position (or into a different program). The mouse is used in text mode under gpm. Text sections are marked by keeping the left mouse button pressed. The marked text is automatically copied into a buffer. When you press the mouse button, the text is pasted at the position of the active insertion point. The right mouse button can be used to change the size of a marked text section.

### Using scroll bars

Many X programs are equipped with standardized scroll bars (for example, xterm). The size of the gray scroll box indicates the relative size of the visible section. While the look is more or less similar, the handling differs from MS Windows standard practice.

The scroll boxes are moved by pressing and holding the mouse button. Clicking the left mouse button moves the scroll box downward, clicking the right mouse button moves upward. The current position of the scroll box indicates how much the scroll box is to be moved; if the mouse is way inside the scroll box, the window contents will be scrolled one line, if it is way down the bottom, the window contents will be scrolled a whole page.

## Making the mouse pointer invisible

Usually, under X the mouse pointer is always visible. Particularly in programs that are primarily operated via the keyboard, this can be rather annoying—pointer often covers characters one would like to see. The remedy is unclutter program. It is started as a background process and automatically hides the mouse pointer when it is located on a window and has not been moved for several seconds. The pointer becomes immediately visible again when the mouse is moved or a mouse button is pressed. In the Debian distribution, unclutter is included in the standard delivery; with most other distributions, the package must be downloaded from the Internet.

## X resources

Resources are a particular feature of the X system - from the background color of an xterm window to the character fonts of most X programs in Emacs. For a better understanding of the concept of resource files, we need to undertake a little excursion into the internals of the X system.

Obviously, there are X programs which use their own configuration files (in addition or exclusively). A frequent reason for not using X resources is the attempt to find a uniform configuration process for different computer platforms. During the search for the greatest common denominator, X resources often fall by the wayside.

## Basics

X programs are composed of so-called widgets. Widgets are graphic control elements for specific tasks. Thus, there are widgets for text fields, buttons, and so on. Widgets have certain features - for example, font for the character set, background for the background color, and so on. Widgets can be embedded hierarchically - for example, inside a frame widget for a menu there can be several widgets for the individual menus.

The complete denomination of an X program detail - for example, the background color of the VT100 widget of the xtterm program - is given by the combination of all components. The components are joined by dots. The following line in the resource file sets the background color to:

```
xtterm:vt100.background:white
```

In X programs, this concept is extended with additional private resources. For this reason, not only can the properties of widgets be changed, but also many global settings (The difference is interesting insofar the setting of widget properties works automatically without having to add a single line of code to the X program). For this reason, man texts for X programs often only describe the program-specific extensions of this resource setting. The following line is a typical example for a program-specific resource setting (here, for the seyon terminal emulator).

```
seyon.hangupBeforeDial:off
```

Another detail of resource setting is worth mentioning: in the composition of names, the wildcard \* can be used. It has the same meaning as in files, but can extend over several components of resource names. For example, the first of the following two lines causes all background areas of every program and widget to be colored yellow, with the sole exception of those widgets which have been explicitly set to a different color. The second line makes all seyon

```
*background:yellow
seyon*background:blue
```

## Resource files

Resource files can be stored in different locations. Depending on the distribution, they are recognized in:

- global settings: /etc/X11/Xresources
- local settings: ~/.Xresources
- current user's settings: ~/.Xdefaults

The font directory also includes the file fonts.dir, which is responsible for the coordination between the font files and the internal font names of X.

![image](img/276_0.png)

## 7.3 X fonts

Management of character sets under X and the use of these fonts is a very complex subject The following information should however, be sufficient to understand the system and add new fonts. If you want to delve deeper into character sets, the following two addresses offer an excellent starting point:

- http://www.gimp.org/fonts/html
- http://www.nwalsh.com/comp/fonts/

Basically, X has non-scalable and scalable fonts. Non-scalable fonts are present as bitmaps in a limited number of sizes (for example, 8, 10, 11, 12, 14, 17, 18, 20, 24, 25, and 34 points). Such fonts can also be displayed in any other size (X simply reduces or increases the characters of the nearest font); however, characters created in this manner look ugly and are very hard to read. In scalable fonts, in contrast, only the shape of each character is described. When a character is used for the first time, the server generates a bitmap of the mathematical description of that character. The quality of the result is good, but the first display may take some time and (when using many fonts and sizes at the same time) require a lot of memory and disk space. Under Windows, fonts generally look smoother than the X Windows System. This is due to the fact that antialiasing is used to draw the characters as grayscale pixels. Unfortunately, the X Windows System does not support antialiasing (version 11, releases 6.3 and 6.4). Individual programs such as gimp, ghostview, xdvi, or acread provide an antialiasing option; however, this effect is achieved via a very time-consuming calculation of the page in a high resolution.

Microsoft Windows is currently still ahead of the X Windows System on an other aspect too: nearly all fonts can be printed on any printer. Under X, this works only in exceptional cases (with some PostScript fonts that are also available as X fonts).

## Font management

Font files are usually located in subdirectories of /usr/X11R/lib/X11/fonts. With non-scalable fonts, there is a separate file for each font size and attribute; with scalable fonts, one file is sufficient for all sizes.

Each font directory also includes the file fonts.dir, which is responsible for the coordination between the font files and the internal font names of X.
