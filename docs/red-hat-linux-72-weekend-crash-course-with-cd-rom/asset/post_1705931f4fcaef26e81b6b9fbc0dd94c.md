
# Ghostscript

![](img/5fe8f856723cde0b366f73584b9e64b8_207_0.png)

10 Min.  
To Go

Ghostscript is a utility for previewing and printing PostScript documents. Ghostscript enables you to print PostScript documents on many non-PostScript devices. At its heart, Ghostscript is an implementation of the PostScript language. Ghostscript includes the interpreter that processes PostScript input and generates output on an output device. A Ghostscript device can be a printer or display screen as well as an image-file format such as BMP or PCX.

Ghostscript is distributed under the GNU GPL, but is copyrighted and maintained by Aladdin Enterprises. Some Ghostscript documentation is installed in the /usr/doc directory. To change to the appropriate directory, type `cd /usr/doc/ghostscript*`. (The exact directory name depends on the version of Ghostscript installed on your system. You can find the latest contact information in the README file in that directory. That directory also contains some other Ghostscript documentation. All of these documentation files are text files that you can view using the `more` command.)

You typically use Ghostscript to load and view a PostScript file. To see how Ghostscript renders a PostScript document, you can use any available PostScript document you have. One good solution is to use one of the sample PostScript files in the `/usr/share/ghostscript/5.50/examples` directory with the `gs` command. (Replace 5.50 with whatever version of Ghostscript is installed on your system.) For example, type the following command in a terminal window:

```bash
gs /usr/share/ghostscript/5.50/examples/golfer.ps
```

Ghostscript opens that file, processes its contents, and displays the output in another window (as shown in Figure 18-4).

In this case, the output is a picture of a golfer. After displaying the output, Ghostscript produces the following message:

```
>>showpage, press <return> to continue<<
```

Press Enter to continue. For a multiple-page PostScript document, Ghostscript then shows the next page. After all the pages are displayed, you return to the Ghostscript prompt. Type `quit` to exit Ghostscript.

# Ghostview

Ghostview is an X-based graphical front end to the Ghostscript interpreter. Ghostview is ideal for viewing and printing PostScript documents. For a long document, you can even print selected pages. You also can view the document at various levels of magnification by zooming in or out.

To run Ghostview, select Main Menu » Graphics » Ghostview (if you are running GNOME), or type `ghostview &` in a terminal window. Both methods open a Ghostview window. The window is divided into three parts:

- Along the window's top edge, you see eight buttons. The first six buttons are menu buttons.
- Down the window's left side, you see several more buttons, text boxes for information display, and scrollbars for scrolling the image.

![](img/5fe8f856723cde0b366f73584b9e64b8_208_0.png)

Figure 18-4 Ghostscript displaying a PostScript file

- The large area occupying most of the Ghostview window is the work area where Ghostview displays the PostScript document.

To load and view a PostScript document in Ghostview, select File » Open or click the Open button on the left side of the Ghostview window. This action causes Ghostview to display a file-selection dialog box. You can choose one of the PostScript files that come with Ghostscript. For example, select the file `tiger.ps` in the `/usr/share/ghostscript/5.50/examples` directory. If your system has a version of Ghostscript later than 5.50, you have to use the new version number in place of 5.50.

To open the selected file, click the Open File button in the file-selection dialog box. Ghostview opens the selected file, processes its contents, and displays the output in its window as shown in Figure 18-5.

In the last two buttons on the upper-right corner of the window, Ghostview displays the current filename and the date the file was created. As you move the mouse over the image, Ghostview displays the coordinates of the mouse pointer in a button along the upper-left corner of the window, which is helpful if you want to select a specific area of the image to edit, copy, or delete.

![](img/5fe8f856723cde0b366f73584b9e64b8_209_0.png)

**Figure 18-5** Ghostview displaying a PostScript file

Ghostview is useful for viewing documentation that comes in PostScript format, which typically uses the `.ps` filename extension. This format is also used for viewing files saved with Adobe's PDF (Portable Document Format) format, which is an increasingly popular file format on the Internet and the World Wide Web. It is very handy to have a single program that can read both file formats. For example, you can use Ghostview to view the documentation for the CVS program, which comes in several PostScript files that you can find in the `/usr/share/doc/cvs*` directory. When viewing such documents in Ghostview, use the magnification button, which is labeled 1.000 in Figure 18-5. If you click that button and hold down the mouse, a menu appears with a number of magnification factors from 0.1 to 10.0. You may have to select a magnification of 2.000 or more to make the document legible onscreen.

## Troubleshooting

If you have trouble persuading `xplayercd` to play CDs for you, you may need to give yourself permission to use the CD-ROM device. To do so, log in as root and execute the following command:

```bash
chmod 666 /dev/cdrom
```

This command gives all users read and write permission to the CD-ROM drive.

If the previous tip brings you no aural joy, try using the actual CD-ROM device, rather than `/dev/cdrom`, which is only a symbolic link. For example, on a sample system `/dev/cdrom` is a symbolic link to `/dev/hdc`, so it would be necessary to execute the following command:

```bash
chmod 666 /dev/hdc
```

If your system has less than 64MB of RAM and you want to use GIMP, setting its tile cache - the amount of RAM it uses for image storage - to a low value, such as 16MB, will improve your system's speed. However, this gain comes at the expense of GIMP's performance, especially if you intend to work with large images. To change the tile cache size, follow these steps:

- Select File » Preferences from the GIMP toolbar.
- Click the Environment item on the Categories tree menu.
- Enter a new value for Tile Cache Size.
- Enable the Conservative Memory Usage checkbox.
- Click OK to save your changes and close the dialog box.

## Review

This session showed you how to configure the sound card and use a few CD-player applications to hear CDs on your Red Hat Linux system. You also familiarized yourself with the GIMP, Xpaint, Ghostscript, and Ghostview applications for working with image files of various formats.

## Quiz Yourself

- How do you employ the `/usr/sbin/sndconfig` utility to configure the sound card for use in Red Hat Linux? (See "Configuring the Sound Card.")
- What steps do you have to perform so that any user can play audio CDs on the CD-ROM drive? (See "Playing Audio CDs.")
- What is "The GIMP" and what can you do with it? (See "The GIMP.")
- How do you view PostScript files with Ghostscript? (See "Ghostscript.")
- How is Ghostview related to Ghostscript? (See "Ghostview.")

# Session 19: Working with the Office Tools in Red Hat Linux

- Using the Gnumeric spreadsheet
- Exploring KOffice applications
- Maintaining calendars
- Working with calculators
- Utilizing the spelling checker

This session focuses on the applications that you need for day-to-day office work. This book’s companion CD-ROMs include all of the Red Hat Linux office tools discussed in this session: calendars, calculators, and spelling checkers. I also introduce you to several prominent commercially available office applications for Linux that are not included on the companion CD-ROMs.

## Using the Gnumeric Spreadsheet

The GNOME desktop comes with Gnumeric, which is an X-based graphical spreadsheet program. To try out Gnumeric, select Main Menu » Applications » Gnumeric Spreadsheet from the GNOME Panel. The Gnumeric program displays its main window, which looks similar to Windows-based spreadsheets such as Microsoft Excel. In fact, Gnumeric can read and write Excel 95 spreadsheet files.

You use Gnumeric the same way as Microsoft Excel. You can type entries in cells, use formulas, and format the cells, specifying the type of value and the number of digits after the decimal point.

You might want to type in a sample spreadsheet to get used to Gnumeric. Try some formulas that you normally use in Microsoft Excel. For example, use the formula `SUM(D2:D6)` to add up the entries from cell D2 to D6. To set cell D2 as the product of the entries A2 and C2, type `=A2*C2` in cell D2.
