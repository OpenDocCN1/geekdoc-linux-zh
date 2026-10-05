
# Changing files are displayed

When you right-click an empty space in the right pane in File Manager, a menu opens with an option to change how the files are sorted. You can sort files by name, modification time, size, or file type, in ascending or reverse order.

You can change how files and folders are shown in File Manager, so you strike a balance between how many you can see at a time and how easy they are to see. The View menu on the bar at the top of File Manager gives you the choice of four ways to display the files and folders in the Folder View mode. By default, File Manager uses the icon, which strikes a balance between the number of files you can see at a time and the size of each icon. The thumbnail preview takes the place of a generic icon for picture files. To see as many files as possible at one time, use the compact view, which fits the files and folders with names and the filename.

The detailed list (see Figure 4-7) reveals more information about each file, showing a short description, its size, and when it was last modified. You can click the column headings to sort the view by the filename, description (which groups similar files), size, or modification date. If you click the column heading again, the sort order is reversed.

![](img/df9a01bf057d58c2401b5edabd6e8829_87_0.png)

| Directory Tree | Name | Description | Size | Modified |
| --- | --- | --- | --- | --- |
| pi | 4row_arrow | PNG image | 9.5 KB | 27/01/15 08:34 |
| college | 4row_black.png | PNG image | 7.3 KB | 27/01/15 08:34 |
| Desktop | 4row_board.png | PNG image | 8.5 KB | 27/01/15 08:34 |
| Downloads | 4row_computer.png | PNG image | 9.5 KB | 27/01/15 08:34 |
| Examples | 4row_red.png | PNG image | 24.8 KB | 27/01/15 08:34 |
| fractive | 4row_be.png | PNG image | 8.7 KB | 27/01/15 08:34 |
| homeback | khatsoft.wav | WAV audio | 36.0 KB | 27/01/15 08:34 |
| Mission | 3webp1.png | Ogg Vorbis | 38.8 KB | 27/01/15 08:34 |
| Pictures | 3webp2.png | Ogg Vorbis | 34.5 KB | 27/01/15 08:34 |
| Public | 3webp3.png | Ogg Vorbis | 37.7 KB | 27/01/15 08:34 |
| | blankpy_game.py | Python script | 308 bytes | 27/01/15 08:34 |
| | cat.png | PNG image | 6.4 KB | 27/01/15 08:34 |
| | importation.py | Python script | 1.0 KB | 27/01/15 08:34 |
| | catgvl.png | PNG image | 7.1 KB | 27/01/15 08:34 |
| | drawing.py | Python script | 1.2 KB | 27/01/15 08:34 |
| | 4row_humanwinner.png (24.8 KB) | PNG image | 19.0 KB | 27/01/15 08:34 |

> FIGURE 4-7:
The detailed list view in File Manager.

LXDE File Manager, written by Hong Jen / Raspberry Pi Foundation

72 PART 2 Getting Started with Linux

Sometimes you might need to refresh the view of File Manager to reflect your latest changes. To do that, tap the F5 key on the keyboard or choose Reload Folder from the View menu.

# Opening a folder in the terminal

Linux has a rigorous permissions structure that governs who can access all files and whether they have permission to modify them or run them. It's a good thing, because it means it's relatively difficult for you to do any harm to your Raspberry Pi's operating system accidentally. You're free to use File Manager to explore all the files your operating system uses, but if you try to delete an essential file, you'll be told you have no permission, as shown in Figure 4-8.

If you want to explore your system, go to your pi folder, click the Up a Level twice (refer to Figure 4-4), and then take a look in the folders there. Chapter 5 covers some of these folders in more depth.

The Tools has an option to open the current folder in the terminal. This enables you to use Linux commands (see Chapter 5) to make changes to the folder. Often, this is the quickest way to accomplish something, especially after you've mastered the finer points of Linux. While you're using File Manager, you can also use the keyboard shortcut F4, to access the terminal.

![](img/df9a01bf057d58c2401b5edabd6e8829_88_0.png)

Figure 4-8: Whoops! Denied permission to delete a file from the Raspberry Pi's boot folder.

# Browsing the Web

When it comes to browsing the web on your Raspberry Pi, you are really spoiled for choice, with four browsers to choose from. The recommended browser, accessed from the Globe icon in the top left of the screen, Chromium. Raspbian also has three other browsers, which you can start by typing their names into the Run option on the Applications:

- **Dillo:** This browser is fast, but web pages look different than intended on because it can't handle sophisticated layout instructions or JavaScript, the language used for creating web pages. Several websites we tried were rendered as a single column because Dillo couldn't understand where the header box, sidebars, main page content, and bottom box should go. You can switch off from the Tools menu, which can quickly speed up downloads of complex pages. If you're accessing mainly text information or have a particularly slow web connection, this.

- **Netsurf:** This is capable of handling more than Dillo, but it lacks JavaScript.

- **Epiphany:** This was the recommended browser for a long time.

![](img/df9a01bf057d58c2401b5edabd6e8829_89_0.png)
