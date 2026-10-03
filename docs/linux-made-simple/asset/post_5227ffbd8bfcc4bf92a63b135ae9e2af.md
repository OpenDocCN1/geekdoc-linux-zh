
## Man pages: Accessing help

Need more advice? Then you need to browse the ultimate collection of useful self-help books that resides inside the Linux operating system.

RTFM has long been considered the battle cry of the supposed Linux experts, and is claimed to scare new users away. If you haven't come across it before, it stands for something like 'Read the fine manual.' It is perhaps easy to appreciate the frustration some individuals feel when asked a question for the umpteenth time when the information is clearly covered in the manual. However, it's only possible for a user to read a program's documentation if they know where to find it. Happily, there are some sources of help within Linux, so let's look at each of them.

Before you even look for the manual, remember that many programs have built-in help. Run the command from a terminal with the --help option to see a synopsis of its options. This applies to GUI programs, as well as shell commands. For example:

```
firefox --help
```

If you need more detail, then it may be time to RTFM, which on Linux systems usually means the man page. Man pages document just about everything on your system and are viewed by keying in the man command. If you want to know how man itself works, the classic recursive example is to open a terminal and run:

```
man man
```

A man page is a single page containing the reference documentation for its topic. The man command renders this document as readable text and displays it in your default pager, usually less. This means you use the same keyboard controls as less for navigating the page: cursor keys to scroll up and down, [Spacebar] to page down, and so on. Some man pages can be very long, so try man bash to enable you to search. In less, press [/] to start searching (or [?] if you want to search backwards), followed by your search term. Then use [n] to jump to the next match or [N] for the previous one. The man pages are divided into sections:

- 1. User commands
- 2. System calls
- 3. C library functions
- 4. Devices and special files
- 5. File formats and conventions
- 6. Games et al
- 7. Miscellany
- 8. System administration tools and daemons

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_117_0.png)

This is the man page for ls, and it helpfully lists the various options that you can use in alphabetical order.

## Desktop viewing

Man and info are intended to be readable in a terminal, because you may need to use them on a system without a desktop. There are GUI viewers for them, though, the most convenient being in KDE, where you can press [Alt]+[F2] and type man:/command or info:/command and get an HTML formatted version of the document displayed in Konqueror. There are also the tkInfo and tkMan programs to display the respective formats in a GUI window.

There are several websites containing comprehensive man page collections: such as http://linux.die.net, www.linuxmanpages.com and http://manpages.ubuntu.com. These are particularly useful if you want to read about something that you do not have installed locally.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_117_1.png)

KDE users can read info and man pages in a browser, with clickable links, thanks to KDE's KIO slaves.

As a normal user, you would normally only use sections 1, 5 and 8 (and possibly 6). If you use the section number with the man command, it will only look in that section, otherwise it will show the first match it finds. This is necessary because you can have more than one page with the same name. The passwd command is used to set user passwords, which are stored in the file /etc/passwd. Try:

```
man passwd
```

```
man 1 passwd
```

```
man 5 passwd
```

The first two document the passwd command from section 1, while the third shows the man page for the passwd file. This is one of the strengths of the man page system – it documents everything: commands, configuration files, library functions and more. It's not limited to specific commands or files, and section 7 contains man pages for all sorts of things. Ever wondered how symbolic links work, or what happens when you turn on your computer? Try:

```
man 7 symlink
```

```
man 7 boot
```

## Quick help

There is more to man than a bunch of formatted text pages and a program to display them in a pager. Man maintains a searchable database of pages, which is automatically updated by Cron, and has some other programs for working with it. Each man page has a NAME section, which includes a short description of the page's topic. The whatis command gives the description – it tells you what the program (or file) is, without going into details of options. Here is the classic geeky, recursive example:

```
whatis whatis
```

```
whatis (1) - search the whatis database for complete words
```

This is a faster way to see what commands do, especially if you want to check more than one:

```
whatis grep sed symlink
```

The whatis command searches only the name, and only matches on whole words, so it assumes you know the name of the command and just want to know what it does. For a more wide-ranging search, use apropos, which does a similar job but searches the descriptions as well and returns all matches – compare these two commands:

```
whatis png
```

```
apropos png
```

There is another form of documentation that's favoured by the GNU project: info pages. While a man page is basically one very long text file with a bit of formatting markup, an info document contains a tree of linked pages in a single file. It's more like HTML than plain text, but is designed for reading in a text console and all the 'pages' are contained in a single file.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_118_0.png)

Unsurprisingly, the command used to read info pages is this:

```
info info
```

This time, the self-referencing is not gratuitous. Man pages are usually quite intuitive to navigate – it's just like reading any other text in a page. Info uses a different set of key commands, so reading its own info page is a good place to start. You move around individual pages as you would normally, but if you press [Enter] when the cursor is on a link (noted by an asterisk), you descend into that node, getting further information on the topic at hand. To go back up to the parent node, press [u]. You can also navigate within a level of the documentation tree with [n] and [p], which take you to the next and previous nodes. If you have ever looked at any GNU documentation online (http://bit.ly/grubmanual) you will recognise this layout. It's simpler than HTML, with the navigation commands generally moving around the same level of the tree or up and down one level.

You may be asking yourself what the point of this structure is. Well, if you've ever tried to find information in a long man page, such as man bash or man mplayer, you'll know how frustrating and time-consuming the 'everything on one page' approach can be. Info documents are divided into sections and chapters, enabling clearer and more succinct presentation. The majority of GNU programs have fairly brief man pages, but have more detail in their info pages. Splitting the document up into pages alters the way that searching is carried out. Press [s] followed by a search string and then [Enter]. Info will jump to the next occurrence of the string, even if it's in a different node. Continue to press [s] then [Enter], with no search string, to jump to subsequent occurrences of the same string. Those keys, plus [q] to quit, should enable you to navigate info pages with ease. You might be wondering why we're not using HTML. The main reasons are that info pre-dates HTML, and that info documents are contained within a single file. Conceptually, they are similar – so much so that info2html (http://info2html.sourceforge.net) can be used to convert an info document to a series of HTML pages.

> The ls info page goes into more detail and groups options according to their function. Info pages generally provide more detail than man pages.

## Printing manuals

There may be times you want a hard copy. As man pages are stored in a markup format and converted for display by the man program, you can use -t to convert them to a printable format, Postscript by default, like this:

```
man -t somecommand | lpr
```

The Postscript is output to stdout; piping it to lpr like this sends it straight to the printer. You could also convert the Postscript to PDF, and therefore create versions of your man pages suitable for carrying around on a tablet or e-reader:

```
man -t somecommand | ps2pdf - somecommand.pdf
```

Print info documents by passing them through the col command:

```
info somecommand | col -b | lpr
```
