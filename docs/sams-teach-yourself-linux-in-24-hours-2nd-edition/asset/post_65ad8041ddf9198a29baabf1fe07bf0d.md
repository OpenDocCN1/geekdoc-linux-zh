
## Using the CRiSPlite Editor

The CRiSPlite editor, included with OpenLinux, is a programmer's editor used mainly to create and edit source code for programming. This editor (an extremely limited version of the commercial editor) sports a graphical interface under the X Window system and features buttons and menus you can use while you work.

Start CRiSPlite by clicking the editor's icon on your desktop's panel if you're using the K Desktop Environment. You can also find an icon in the initial Looking Glass desktop after you start an X session with the fvwm2 window manager. Start the editor from the command line of a terminal window with the mcr command, like this:

```
# mcr
```

The editor appears with its window, as shown in Figure 14.7.

### FIGURE 14.7
The CRiSPlite editor for OpenLinux is mainly a programming editor.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_345_0.png)

You can also use this editor from the command line of your console with the cr command, like this:

```
# cr
```

Press Enter to launch CRiSPlite without the X Window System.

## StarOffice's StarWriter

The StarWriter component of the StarOffice suite of productivity programs (shown in Figure 14.8) for OpenLinux is a professional and capable word processor. This program (used, in part, to write this book) is installed along with StarOffice from this book's CD-ROM. This editor supports nearly all the features found in more expensive word processors for other operating systems.

### FIGURE 14.8
The StarWriter component of the StarOffice suite of tools for OpenLinux is a professional word processor.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_346_0.png)

To install StarOffice 4.0, insert your OpenLinux CD-ROM, and then mount the CD-ROM like so:

```
# su -c "mount /mnt/cdrom"
```

Navigate to the StarOffice installation directory on the CD-ROM, like so:

```
# cd /mnt/cdrom/Star*/english/prod_lnx
```

At the command line, use the StarOffice setup command to start the installation, like this:

```
# setup
```

Press Enter to start the installation.

> If you receive the newer StarOffice 5.0 suite, first browse to http://www.stardivision.com to obtain a customer number and registration key. You need to enter your customer name, customer number, and registration key exactly as shown on the StarDivision registration page in order to install and enable StarOffice 5.0. See Hour 19, "Home Office Management with StarOffice," for more details about installing and using StarOffice.

StarOffice installs in an OfficeXX directory in your home directory, where XX represents the version of StarOffice installed (40 for 4.0 or 50 for 5.0). Start StarOffice by typing the following:

```
# Office50/bin/soffice &
```

To create a new StarWriter document, click the StarOffice Start menu (at the bottom left of the StarOffice desktop). StarWriter appears, as shown in Figure 14.8.

## Corel's WordPerfect for Linux

OpenLinux is a great Linux distribution to use, and now there's an even better reason to use Linux: In December 1998, Corel, Inc. released the WordPerfect version 8 word processor for free for personal use with the Linux operating system. WordPerfect, one of the most mature and capable word processors on the market today (for any operating system) can be downloaded, installed, and used for free.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_347_0.png)

> You should definitely register your copy of WordPerfect, even if you only use it occasionally. Corel, Inc. needs to have an accurate idea of the potential of the Linux software market, and your registration helps encourage development of new commercial software for Linux. Corel, Inc. is to be applauded for making this software available at little cost to the casual Linux user.

To get your copy, browse to http://www.linux.corel.com/linux8/index.htm. Follow the links, read the installation instructions, and then download and install the file GUI.tgz (nearly 24 megabytes in size). You can then start WordPerfect by typing the complete path to the executable file (using the installation directory specified during your WordPerfect installation), like so:

```
# /opt/wp/wpbin/xwp &
```

The WordPerfect splash screen appears, along with a control dialog box and the blank WordPerfect document window, as shown in Figure 14.9.

### FIGURE 14.9
The distribution of the WordPerfect 8 word processing system for OpenLinux represents Corel, Inc.'s concerted investment and confidence in the worldwide Linux user community.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_348_0.png)

## Applix Words

There are many other Linux word processing programs besides the text editors installed on your system. These programs are in the public domain, distributed as shareware, or sold commercially. One word processor, Applix Words by Applix, Inc., has many different features:

- It is an integrated part of the Applixware suite of office tools, including a spreadsheet, graphics, mail, and presentation program and supporting frames, linked objects, and pasted graphics.
- It provides a WYSIWYG view of your documents and comes with two dozen fonts.
- It imports and exports 20 different word processing file formats.
- It supports extensive editing macros.
- It includes a spelling dictionary and thesaurus.
- It includes extensive built-in and context-sensitive help.
- It creates and edits hypertext markup language, or HTML documents.
- It can be completely customized with new menus or keyboard commands.
- It builds indexes, tables, tables of contents, and glossaries.

Applix Words requires the X Window System. The Applixware suite needs about 135 megabytes of your hard drive space and 16 megabytes of your computer's memory to run comfortably. After installing Applix Words from the Applixware CD-ROM, run it with the following:

```
# applix -wp
```

> The latest version of Applixware (4.4.1 at the time of this writing) has an installation and execution problem related to OpenLinux 1.3. This problem involves Caldera's use of older versions of shared software libraries. Fortunately, you can install Applixware and then configure its libraries to work with OpenLinux 1.3. First, log in as the root operator, and then navigate to the /opt/applix/jre15/lib/i386/green_threads directory. Use the mv command to rename the library file libd1.so.1 to libd1.so.1.dontuse. Next, open your .bashrc file in your home directory, and enter this new environment variable definition: export LD_PRELOAD=/lib/libd1.so.1. Log out and log back in to OpenLinux to use the new definition. You can now use Applixware!

This command line starts the word processor component as shown in Figure 14.10. Applix Words also has a tutorial, like emacs. To start learning, select the Help menu, and then pull down the Tutorial menu item. (You also can hold down the Alt key, and then press H, followed by the T key.)

### FIGURE 14.10
The Applix Words program is a WYSIWYG word processor including a customizable interface and professional editing tools for writers.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_349_0.png)

Find out more about Applix Words and the Applixware productivity suite for Linux by browsing to the following site:

http://www.applix.com.

## Changing Text with sed and Other Filters

Until now, this hour has discussed interactive editors featuring cursor movement, menus, or other keyboard commands. There are several other programs, such as text filters, or stream editors, included with your system that can edit text.

If you read the discussion in Hour 6, "Using the Shell," you'll recall that many Linux programs can use your shell's standard input and standard output. By using shell operators, such as pipes or redirection operators, you can use Linux commands to filter text through pipelines to manipulate or change the text stream. There also are several other programs, such as ex and sed, that are specifically designed to edit filtered text and are called stream editors.

Thanks to the FSF folks, the GNU text-utils package of two dozen text utilities is also installed on your system. This collection includes cat, cksum, comm, csplit, cut, expand, fmt, fold, head, join, md5sum, nl, od, paste, pr, sort, split, sum, tac, tail, tr, unexpand, uniq, and wc.

Some of these formatting commands, such as fmt and pr, are discussed in the next hour, "Preparing Documents," but this section shows you how you can use several others to manipulate text. For example, the tr, or transliterate, command can be used to work on streams of text to translate, squeeze, or delete characters.

The tr command works by taking sets, or lists of characters on the command line, and using them to translate input text. If you have a document containing uppercase and lowercase but want to change the text to all uppercase, you can tell the tr command to do this by specifying the two sets of characters. A public domain software license (found in the /usr/doc/shadow-misc directory) is used in the following example:

```
# cat LICENSE
...
1. You may make and give away verbatim copies of the source form of the Standard Version of this Package without restriction, provided that you duplicate all of the original copyright notices and associated disclaimers.

2. You may apply bug fixes, portability fixes and other modifications derived from the Public Domain or from the Copyright Holder. A Package modified in such a way shall still be considered the Standard Version.
...
```
