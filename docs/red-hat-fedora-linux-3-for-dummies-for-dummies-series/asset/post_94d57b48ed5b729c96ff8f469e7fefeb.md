
## Creating files and directories

Right-click anywhere in a Nautilus window and select **Create Folder**. A new folder (*directory* in Linux terms) is created and named untitled folder. Right-click the new folder, select **Rename**, and enter any name you want for the directory.

To create a file, right-click in the Nautilus window and select **Create Document Empty File**. The new file icon appears and you can type in its name.

## Viewing files and directories

Files and directories are displayed on-screen as icons by default. The only information an icon shows is the name and whether an item is a file or directory. You can display files and directories as a list by choosing **View View as List**.

This list describes the differences between views:

- **View as Catalog**: Selecting this option displays thumbnail images of any graphical images stored in the current folder. This option isn't active when no images are stored in the current folder.
- **View as Icons**: The default display option; shows the icon and indicates whether an item is a file or directory. Regular file icons take several forms, but text and configuration files look like pieces of paper with a corner folded. Files containing specific types of data have small subicons overlaid on the file icon. For example, PDF files have a PDF subicon. Links, devices, and other objects take other forms. Directories take the form of a partially open manila folder. Icons are evenly placed across the entire File Manager screen. Icons tend to make distinguishing files and directories easier, but take up more space on-screen.
- **View as List**: Displays the size and time stamp of each file and directory in addition to their names.

![](img/41feae212f5c6612ff709354891f7b39_147_0.png)

You can use Nautilus to create more shortcut icons on your desktop that point to files or applications. In Nautilus, just click and drag any file or application to any blank part of the desktop and then release the mouse button. An icon is placed on the desktop. You can then start the application by double-clicking its icon. If the icon points to a data file (a text file, for example) and Nautilus knows how to handle its MIME type, Nautilus launches the appropriate application to open the file. Otherwise Nautilus prompts you to specify which application to use to open it.

Technical stuff
Nautilus is programmed to recognize numerous Multipurpose Internet Mail Extensions (MIME) types, and they define which type of information a file stores in other words, MIME keeps its own Rolodex of sorts. Each MIME type is associated with certain file extensions. For example, when you double-click a .doc file, Nautilus recognizes that the .doc file suffix corresponds to a Word document MIME type and opens the OpenOffice word processor (as described in Chapter 13), which loads the .doc file.

## Running programs

Nautilus is such a hard worker that it happily launches commands for you. You simply right-click the icon you want to run, which opens a submenu, and then you choose Open. For example, if you click the xclock icon in the `/usr/bin/X11` directory, xclock appears on your desktop. (Double-clicking the icon performs the same function.)

Managers are generally not very smart. But Nautilus is smarter than the average bear, and it knows what to do when it encounters various file types. If you open a non-executable file, such as a PDF file, File Manager knows which program to use in order to view it.

## Introducing Fedora Core/GNOME Applications

Numerous applications are installed during the installation process described in Chapter 3. The following sections list each installed application and a short description of their function. Each section corresponds to the submenu you see when you click the GNOME Menu.

### Accessories

You'll find miscellaneous applications in this submenu. The following list provides a short description of each application.

- **Calculator.** This is the Gcalc tool application. Gcalc tool provides three calculator modes: basic, financial, and scientific. It also includes ten storage registers.
- **Dictionary.** This is a network-based client application that looks up word spelling and definition via the MIT dictionary server—dict.org.
- **Text editor.** Gedit provides a simple, effective text editor.

### Games

Okay, Linux was initially oriented toward running services, so it may not seem ideal for game players. But indeed, it has lots of games. Open the Games icon and you see many of them. You'll find that you can waste your life with Linux just as easily as with Windows! Ha!

The following list gives a short description of each game:

- **AisleRiot Solitaire.** This game allows you to play several versions of Solitaire.
- **Ataxx.** This is a board game for two players; you play against the computer. The object is to flip discs until your opponent doesn't have any more discs. This game is similar to Reversi.
- **Blackjack.** This game, you guessed it, allows you to play Blackjack.
- **BZFlag.** You get to shoot tanks! Ah, to be 13 again.
- **Five or more.** Theoretically have fun by removing colored balls.
- **Four-in-a-row.** You have to create a line of four marbles. Your opponent, real or computer, has to do the same. First line wins.
- **Freecell Solitaire.** This is another Solitaire game.
- **FreeCiv client and server.** Figure a strategy to destroy other civilizations. You must start the FreeCiv server before starting the game by running a FreeCiv client.
- **Igno.** This is another disc-flipping game similar to Ataxx.
- **Klotski.** Move a patterned block to accomplish some objective. If you have a lot of time on your hands, you may find this game interesting.
- **Maelstrom.** You fly your spaceship through an asteroid belt to win this game.
- **Mahjongg.** This is a single-player version of the classic Mahjongg Eastern tile game.
- **Mines.** In this game, you need to clear space through a minefield.
- **Nibbles.** You control a snake and try to get it to eat diamonds.
- **Robots.** There are robots out there whose goal is to kill you. Your goal is to — yep, you guessed it — avoid death.
- **Same GNOME.** You get a window full of balls. You must remove as many balls as efficiently as possible.
- **Stones.** In this arcade game, you must pick up as many stones (they're gems) as possible while avoiding falling stones.
- **Tali.** In this game, you roll dice and "create" a poker-like hand.
- **Tetravex.** You must solve a puzzle in this game.
- **Tux Racer.** This is actually a fun and popular game. Tux Racer is actually Tux the Linux Penguin who races down snow-covered mountains.

### Graphics

You can view and manipulate graphical images with several utilities. Click the GNOME Menu and then the Graphics menu and you can run applications like The GIMP (An excellent tool for working with and editing images). You can use the Scanning tool to scan images on a scanner and use the digital camera tool to upload pictures from your camera.

- **GIMP Image Viewer**. The GIMP (GNU Image Manipulation Program) is a powerful image program that opens, displays, and manipulates graphical files of numerous formats. There are far too many manipulation functions to list here.
- **PDF Viewer**. The GNOME PDF Viewer opens and displays Portable Document Format (PDF) files.
- **Photo Tool**. This application helps you to download and store photographs from your digital camera.
- **PostScript Viewer**. The Gnome Ghostview displays Postscript files.

### Help

This application provides a Nautilus window that contains links to information about the GNOME desktop, applications, and development tools, as well as general and system-info topics.

### Internet

Evolution is the new Fedora Core default e-mail client, which is found in this submenu. You also find Mozilla and some other Internet applications here.

- **Evolution Email**. Selecting this menu option starts the Evolution e-mail client. See Chapter 11 for more information on this application.
- **Gaim Internet Messenger**. This is an instant-messaging client. You can use this application to communicate with other instant messengers that use AIM, ICQ, Yahoo!, MSN, Jabber, IRC, Napster, Gadu-Gadu and Zephyr.
- **IM**. This chat client can communicate using several protocols.
