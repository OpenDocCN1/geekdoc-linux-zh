
# 16.1.1 Selecting an X Font Name

X font names can be long and difficult to type; to make it easier, use the `xfontsel` client, an interactive tool for picking X fonts and getting their X font names.

When you start `xfontsel`, it looks like Figure 16-1 (the window frame will differ depending on your window manager).

![](img/be7f02611e5cefde1a18c788fede22f7_430_0.png)

*Figure 16-1. Starting xfontsel.*

The row of buttons are pull-down menus containing options available on your system for each field in the X font name. Use the mouse to select items from each menu, and the X font you have selected is shown in the main window. Above it is written its X font name.

⇒ To make the X font name the X selection, click the mouse on the button labeled `select`.

This example makes the X font name the X selection, which permits you to paste the X font name on a command line or into another window (see Recipe 10.3.2 [Pasting Text], page 254).

## 16.1.2 Listing Available X Fonts

Use `xlsfonts` to list the X font families, sizes, and weights available on your system. Supply a pattern in quotes as an argument, and it outputs the names of all X fonts installed on the system that match that pattern; by default, it lists all fonts.

⇒ Here are some ways to use this.

- To list all the X fonts on the system, type:
  
  `$ xlsfonts` ↵

- To list all the X fonts on the system whose names contain the text “rea,” type:
  $ xlsfonts '*rea*' RET
- To list all the bold X fonts on the system, type:
  $ xlsfonts '*bold*' RET

NOTES: This is not a way to display the characters in a font; for that, use xfd, described next. Furthermore, to browse through available X fonts, you want to use xfontsels, as in the previous recipe.

## 16.1.3 Displaying the Characters in an X Font

Use the xfd (“X font display”) tool to display all of the characters in a given X font. Give the X font name you want to display in quotes as an argument to the -fn option.

⇒ To display the characters in a medium Courier X font, type:
$ xfd -fn '-*-courier-medium-r-normal-*-100-*-*-*-*-iso8859-1' RET

## 16.1.4 Resizing the Xterm Font

See Recipe 4.2.3 [Specifying X Window Font], page 104, for information on specifying the font for X client windows. One of the tools it is most useful to specify a font for is xterm, which is usually used to run a shell while in X; many people like to specify which font is used for this window (see Recipe 4.5 [Getting a Terminal Window in X], page 109).

To resize the current font when the xterm is running, press and hold CTRL and right-click anywhere in the xterm window. A menu will appear that gives you the size options, from Unreadable and Tiny to Huge. To resize the font to its original size, choose Default.

## 16.2 Using TeX Fonts

The following recipes pertain to TeX fonts in particular.

## 16.2.1 Listing Available TeX Fonts

A popular question among new TeX users is how to list all of the TeX fonts installed on the system—most installations come with a lot of them, and it would be helpful to easily list and display them all. Unfortunately, there is no uniform and surefire way to do it. You can use many types of fonts

with TeX, and the precise fonts installed will differ from system to system. TeX fonts are typically stored in the /usr/share/texmf/fonts/ and /usr/local/share/texmf/fonts/ directory trees.

To get a list of TeX fonts on your system, use locate to list files with a .tfm extension. These are TeX font metric files. Not all of the TeX fonts have a .tfm file, and not all of the .tfm files are usable fonts, but you can get a good idea of the TeX fonts installed on your system with this method.

⇒ To list the available .tfm fonts on your system, type:

```
$ locate .tfm RET
```

NOTES: You may want to redirect the output to a file, or peruse it with less in a terminal window of its own, while you use this output to display samples of the fonts as described in the next recipe.

## 16.2.2 Viewing a Sample of a TeX Font

The file /usr/share/texmf/tex/plain/base/testfont.tex, included with TeX, is a special TeX file you can use to display a sample of any .tfm font.

When you process this file, it asks for the name of a font to display. Give the base file name—that is, omit both its path and extension. Then type \sample and \end, each on lines of their own, TeX commands that first print the sample and then end the TeX file. This command will create a DVI file in the current directory named testfont.dvi that contains a sample of the letterset for the given font.

⇒ To view a sample of the plu10 font, type:

```
$ tex /usr/share/texmf/tex/plain/base/testfont.tex RET
This is TeX, Version 3.14159 (Web2C 7.3.1)
(/usr/share/texmf/tex/plain/base/testfont.tex
Name of the font to test = plu10 RET
Now type a test command (\help for help):)
* \sample RET
[1]
* \bye RET
[2]
Output written on testfont.dvi (2 pages, 12344 bytes).
Transcript written on testfont.log.
$ xdvi testfont.dvi RET
```
