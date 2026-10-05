
## Special features of the X version xman

xman is normally run as a background program, so that work in the terminal window is not affected. xman & with the cory charm of early X programs - displays a small control window, which shows a help text about the usage of xman when you click the HELP button. The MANUAL PAGE button leads to a bigger window in which the required help text can be selected. Unlike man, it is not possible to pass xman the required help subject as a parameter at calling time.

```
xman [options]
```

- -bothshown divides the main window into two sections (subject list and help text).
- -notopbox starts xman without the control window.

In the main window, via the SECTION menu, a list of texts available for each of the nine help subject areas can be viewed. The required subject is selected by clicking on it with the mouse.

The most interesting man command is SEARCH. It rapidly searches and displays required help subjects. When the search is stopped with the APROPOS button, xman displays a list of subjects containing the search. However, the Apropos search is not a full text search. Only the keywords of each man text are searched through.

xman supports the mouse not only to select and scroll through texts. With Shift and the middle mouse button can quickly toggle between the subject list and the displayed man text. Ctrl and the middle mouse button display the OPTIONS menu.

The keyboard shortcuts of xman, unfortunately, do not correspond to those of man. In particular, the cursor keys cannot be used to scroll through the help text. The following table summarizes the available shortcuts:

xman keyboard shortcuts

| Key | Description |
| :--- | :--- |
| F B | one page forward or backward |
| Spacebar | one page forward |
| I to 4 | one to four lines forward |
| Ctrl+S | search manual text |

## tkman

Like xman, tkman provides an X interface for the display of man pages. Once the installation of tkman has succeeded (it requires the programming languages Tcl and Tk to be installed, amongst others), tkman offers the following advantages over xman:

## man - THE ONLINE MANUAL FOR ALL COMMANDS 73

![](img/b30873dd3d753687a59253fb9ad26a0b_100_0.png)

Figure 4.1 Reading man texts with xman.

- - Easy cross-referencing to other pages by simple double-clicking highlighted-texts.
- Management of a list of all recently viewed man texts.
- Easy search within a man text.
- Possibility of highlighting pieces of text and storing these highlights permanently.
- Extensive configuration possibilities.

![](img/b30873dd3d753687a59253fb9ad26a0b_100_1.png)

Figure 4.2 Reading man texts with tkman.

## man internals

The central file for man is /etc/man.config. In this file, the paths for various files are set. This file also contains the specification that the less program is used to display the man texts. (For this reason, the keyboard commands of man and less are the same when a text is displayed.)

Generally, there is no need to modify man.config. If you want to specify additional directories to be searched by man, you can set the MANPATH environment variable in /etc/profile accordingly. In the standard configuration, man searches the following directories for man texts:

```
/usr/man
/usr/local/man
/usr/X118/man
```

Each of these directories has subdirectories man1 to mann containing the source texts. To be able to display these texts on screen, the groff program must be used to convert them into ASCII format. To avoid repeating this conversion for each access to a man page, the formatted texts are stored in their own directories (either cat in the directories mentioned above, or in a sub directory /var/man or /var/catman). Sometimes, man texts are only stored in their format (to save space)—but this is a disadvantage if the texts are to be printed.

The configuration of xman can be further modified by entries in the /.xdefaults or /.Xresources file (see the xman manual text).

> Information on conversion of man source files into readable ASCII documents or PostScript files can be found on page 511.

## 4.2 info – hypertext online help for GNU utilities and Emacs

info is a much more powerful program than man. It is particularly suitable for displaying voluminous help texts, as it can cope with cross-references across several files. info is the preferred documentation format for all GNU tools (such as find, grep), for the GNU C compiler with all extensions and libraries, and for the Emacs editor.

> Instead of info, you can also use emacs or xacs and use Alt+X to change into info mode (see also page 546). The main advantage is that you can use the mouse to follow links, which are highlighted in a different color.

Generally, info texts are stored in the /usr/local/info directory (depending on the system, also in /usr/share/info or /usr/share/info). Larger help texts are normally distributed across several compressed files whose end in .info-nn.gz or only in -nn.gz.

## info - HYPERTEXT ONLINE HELP GNU UTILITIES AND EMACS 75

info [Options][subject]

info is normally called with the parameter subject. The subject indicates which info file of the /usr/info directory is to be viewed. If info help started with no parameters, the program displays an overview of the available help files (/usr/info/dir). Subjects not contained in dir can be viewed with the option -f. This is, for example, for the elisp files (documentation about Lisp programming for Emacs). Thus, info cannot automatically handle all info files contained in /usr/info.

-f file

loads the specified file instead of a file from /usr/info. Instead of a subject, the full file name must be given (jarg300.info.gz, not just larg300). If the info text is distributed across several files, the first file must be specified (for example, elisp-1.gz).

## info keyboard shortcuts

| Key | Description |
| :--- | :--- |
| Spacebar | scroll text down |
| Backspace | scroll text up |
| B | |

> info comes with a man text, which describes the basics of handling the program. The internals of info files and oninfo can be found on page 512. With texi2html, you can convert info files into HTML format - see page 513.

If you have installed GNOME or KDE you can also read info texts very easily by using the corresponding help system. The following examples show how the info text is displayed:

```
user$ gnome-help-browser info:emacs
user$ gnome-help-browser toc:info
user$ kdehelp info:(emacs)
user$ kdehelp info:(dir)
```

## 4.3 Linux-specific online documentation

## Reading documentation in other formats

Linux-specific online documentation is available in the most varied formats. The following list gives some hints on the best way such documents can be read:

- ASCII: These texts can be read directly with less or any other editor. The programs a2ps or mpage allow conversion into a PostScript file.
- PostScript format (*.ps): These files can be read with ghostview or khostview. With gs, you can produce a printout if you do not own a PostScript printer.
- DVI format (*.dvi): Such files are the result of Teor LaTeX conversion and can be read with vinho or kdvi, dvips allows conversion into PostScript files.
- HTML format (*.html): These files can be read with any WWW browser (Lynx, Netscape, kdehelp).
- Adobe Acrobat format (*.pdf): This is a compressed variation of the PostScript format, which has imposed itself particularly Internet documents with sophisticated layout. The files can be read with ghostview, khostview, xpdf or acroread.

In all versions, except for the last one, files may be compressed. Such files can be recognized by their extension .gz or .bz2. They execute gunzip file.gz or bunzip2 file.bz2. This replaces the compressed file with its uncompressed version. Sometimes, several files are combined into one common archive (extension .tar), which is usually compressed as well (extension .tgz).

The programs mentioned above are not used only for reading online documentation and are therefore described elsewhere in:

| Program | Reference |
| :--- | :--- |
| Less | page 139; some keyboard shortcuts as man (page 71) |
| ghostview, khostview | PostScript viewers, page 518 |
| xdpi, kdvi: DVI viewers, page 520 |
| dvips: DVI → PostScript conversion, page 507 |
| Lynx, Netscape, kdehelp: Internet tools, page 326 |
| acroread: PDF viewer, page 522 |
| bunzip2, gunzip, tar: Standard commands, pages 443, 460, and 483 |

## FAQ – Frequently Asked Questions

Under Linux, FAQs play only a secondary role compared to the HOWTO texts. On the Internet, you will find innumerable FAQs regarding various programming languages, networking questions, and other Unix subjects (security). To decompress and so, gen-
