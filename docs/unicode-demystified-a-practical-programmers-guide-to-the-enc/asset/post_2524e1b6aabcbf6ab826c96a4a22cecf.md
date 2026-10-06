
To find out about a utility, including the man utility itself, give the command man, followed by the name of the utility. For example, the following command displays information about the utility:

```bash
man who
```

Under the X Window System (running GNOME or KDE, for example), you can use xman, which provides a GUI to the man pages. Start xman when you want xman to run in the background from a terminal emulator. Use xman& when you want xman to run in the background and you can use the window while xman is running. Either way, a small xman window appears when you move the mouse pointer over and click Manual Page at the bottom of the window, xman displays a larger window, named Manual Page, that contains xman Help (Figure 2-5).

![](img/aa8214d49e1cf50152c432845129fb3b_92_0.png)

Figure 2-5 xman Help page

Other graphical tools for reading GNU/Linux manual are the GNOME help system (page 204) and the KDE Khelper (page 269). These browsers are more sophisticated than xman and include such features as the ability to move quickly from one page to another by using hypertext (page 1472) links.

Based on the FHS (Filesystem Hierarchy Standard, page 112), the GNU/Linux system manual and the man pages are divided into ten sections. Each section relates tools:

- 1. User Commands
- 2. System Calls
- 3. Subroutines
- 4. Devices
- 5. File Formats
- 6. Games
- 7. Miscellaneous
- 8. System Administration
- 9. Local
- 10. New

This layout closely mimics the way the set of UNIX manuals has always been divided. Unless you specify a manual section, man displays the earliest occurrence in the manual of the word you specify on the command line. The xman utility requires that you specify the manual section you want to look in. Most users use the information they need in sections 1, 6, and 7; programmers and system administrators frequently need to consult the other sections.

In some cases there are manual entries for different tools with the same name. For example, the following command displays the manual page for the write utility (page 84) from section 1 of the system manual:

```bash
$ man write
```

To see the manual page for the write system call from section 2, enter

```bash
$ man 2 write
```

This command instructs man to look only in section 2 for the manual page. Use the -a option (press q to move to the next section) to view all the man pages for a given subject; use man -a write to view all the man pages for write.

# Documentation 45

```
Terminal
info Edit Search Help Menu
file: dir.

info (the Directory node) gives a menu of major topics.
  'q' exits, 'p' lists all commands, 'h' returns help.
  '?' for help instructions.
  '*manual' visits the emacs manual, etc.
In info, you can click button 2 on a menu item or cross reference to select it.
* Menu
  GNU admin
* (autotake) Making Makefile.in
* individual utility
* local (autotake) Generating a local.at
* libtool (libtool) Adding libtool support.
* manuals
* an (man)
* (info) The info file descriptor library.
* info: (dir) display the top lines
Welcome to info version 4.3. Type for help: for menu items.
```

Figure 2-6 The screen that info displays

# info: Displays Information

The character-based info utility is a menu-based hypertext system developed by the GNU project and distributed with Red Hat Linux. You can call this utility from the emacs editor or as a stand-alone program as described here. The utility includes a tutorial on itself (give the command info or go to www.info.org/manual/info/html/mono/info.html) and documentation on many GNU/Linux shells, utilities, and programs. Figure 2-6 show the screen that info displays when you give the command info. Because the information on this screen is drawn from an editable file, you may see a different display. When you see the info screen, editor, you can press

- * h to go through an interactive tutorial on info
- ? to list commands
- SPACE to scroll through the menu of items you can get information on
- m, followed by the name of the menu item you want to go to
- q to quit

The notation that info uses to describe keyboard keys may not be familiar to you. At the bottom of Figure 2-6 are the words “C-h” for help: Hold down the CONTROL key and press h to get help. Similarly, M-x holds the META or ALT key

7. An option modifies the way a utility or command works. Options are specified as one or two hyphens (there are exceptions) preceded by one or two hyphen. The option appears following the name of the utility you are using and a SPACE. Any other arguments (page 1454) to the command follow the option and a SPACE. For more information, refer to “Options” on page 139.

# Chapter 2 Getting Started

![](img/aa8214d49e1cf50152c432845129fb3b_95_0.png)

Figure 2-7 The screen displays after you SPACE a few times and press x. Refer to "Keys: Notation and Use" on page 48 for more information on.

After starting info, press the SPACE a few times to scroll the display. The asterisk at the end of the line means that this is the beginning of a menu item. Following the asterisk is a colon, the name of the package (in parentheses) that belongs to, other information, and on the right, a description of the item. The name of the item is what you type in a command to view, followed by RETURN. When you type m (for name), the cursor moves to the bottom of the window or screen and displays sleep on that line, and pressing RETURN takes you to the item you have chosen. Figure 2-8 shows the top node of information that you can scroll through with SPACE. To get to the next node, press n. Press p to get the previous node. You can always press d to get the initial menu, shown in Figure 2-6. As you read and learn about new utilities, you can use man or info to find out you may have access to hardcopy GNU/Linux manual, the electronic copies are generally more-to-date. If you can print PostScript documents, you can print a manual page with the utility using the -t option (for example, man -t lpr). Better yet, use your browser to look at the documentation on Red Hat Documentation CD-ROM (page 48).

8. On some systems you need to press ESC and then x to duplicate the function of META-x.
9. In most cases corresponds to the name of the package (page 92) containing the file.

# HOWTOs

![](img/aa8214d49e1cf50152c432845129fb3b_96_0.png)

A HOWTO explains in detail how to do something related to GNU/Linux, from setting up networking to administration specialized hardware. Mini-HOWTO offer shorter explanations. As GNU/Linux software, one person or a few people are generally responsible for HOWTO, yet many people contribute to it. The Linux Documentation Project (LDP) site hosts all HOWTO and mini-HOWTO. From a GUI, use your browser to go to www.ldp.org, click HOWTOs, and pick the index you want to find HOWTO or mini-HOWTO. Or use the LDP search feature on its home page to find HOWTOs and More. From a character-based interface, use ftp to open ftp://iblio.org and go to /pub/Linux/docs/HOWTO to download versions of HOWTO.

# Other Sources of Help

KDE and GNOME tooltips (page 182), which display context-sensitive help in a GUI environment. GNOME provides an integrated help system (page 204), and KDE provides What's? button (page 269), the HelpCenter (page 269), and Menu selections (page 270).

# Your System

The /usr/share/doc and /src/linux*/Documentation directories often contain different information about a utility that does man or info.

10. Only present if you installed the kernel source code. Frequently this information is meant for people who will be compiling and modifying the utility, not just using it. These directories hold more than 500 files and directories, each containing information on a separate topic.

# Red Hat Documentation CD-ROM

Unless it mounts automatically, the easiest way to work with the Hat Documentation CD-ROM is to mount it from a terminal emulator with

```bash
$ mount /mnt/cdrom
```

Then point your browser toward /mnt/cdrom and click index.html (xx the language code, just as for English). From there you can choose the manual and format you want.

# Documentation CD-ROM Useful Only from GUI

The files on the Documentation CD-ROM are useful only from a GUI. They cannot be read on a character-based terminal. You can read the Documentation CD-ROM on another system, such as MS Windows, and use the tools to open the files. Click the index.html file to get started.

# Internet

The Internet provides many helpful sites. Aside from sites that carry various forms of documentation, you can enter an error message that you are having a problem with a search engine as Google (www.google.com). Enclose the error message within double quotation marks to improve the quality of your results. You will likely find e-mail concerning “your” problem and how to solve it.

# The Red Hat Home Page

The Hat home page (www.redhat.com) has a wealth of information. Click Support and Docs to view a list of online documentation specifically for Red Hat. All manuals are online at www.redhat.com/docs.

- Support forums are online discussions about any Red Hat-related issues that people want to raise. One forum is dedicated to new users; others to Apache, X Window System, and so on. From the Red Hat home page, click Support and Docs then Support Forums (upper left). Choose About these forums and then A Guide to Web Crossing for a tutorial on using the support forums.
- Hardware help is available by going to Support and Docs Support ResourcesHardware Compatibility (see the Support Links).
