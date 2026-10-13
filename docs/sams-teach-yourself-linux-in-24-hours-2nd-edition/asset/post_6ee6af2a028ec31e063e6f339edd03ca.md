
## NEW TERM

Notice that the nroff command is used on the command line instead of groff. This is because the nroff command installed on your system is a shell script, written to use the GNU groff formatting program to emulate the nroff command. All OpenLinux man pages are written using a special set of nroff commands called man macros. You can use the groff command to use man macros to format your own manual pages. For example, if you create a manual page for a new game called nw, the manual page, called nw.6, might look like the following:

```
.TH Nano-Warrior 6 Games 1/1/98 Linux
.SH NAME
nw - play Nano-Warrior
.SH SYNOPSIS
nw
.B -d
.PP
-d = play deathmatch mode
.SH DESCRIPTION
.PP
The nw command is used to play a game of Nano-Warrior on your Linux console. Play continues until you are wiped out by hordes of alien invaders swarming down the screen.
.PP
Don't give up the fight!
.SH FILES
/usr/games/nw
.PP
$HOME/.nw_scores
.SH BUGS
Probably too many.
```

You can process this manual page and send it to your display with the following:

```
# groff -Tascii -man nw.6
```

```
Nano-Warrior(6)               Linux                       Nano-Warrior(6)

NAME

nw - play Nano-Warrior

SYNOPSIS

nw -d
    -d = play deathmatch mode

DESCRIPTION

    The nw command is used to play a game of Nano-Warrior on
your Linux console. Play continues until you are wiped out
by hordes of alien invaders swarming down the screen.

    Don't give up the fight!
```

FILES

/usr/games/nw
$HOME/.nw_scores

BUGS

Probably too many.

Notice that the man page macros boldface the sections and format the following text automatically. A list of these and other manual page macros are found in the man.7 manual page under the /usr/man/man7 directory. You can read this manual page with the following:

```
# man 7 man
```

The groff formatting program also comes with other sets of typesetting macros, such as the me, mm, or ms manuscript macros used to format text files. You generally need to specify the macro set on the groff command line if you use these commands:

```
# groff -Tascii -mm myfile.txt
```

Documentation for several of these macros is on various manual pages related to groff. One of the best documented sets included with your OpenLinux distribution is the collection of mm manuscript macros on the groff_mm manual page. Table 15.2 lists some common macros you can use to produce formatted documents.

## TABLE 15.2 COMMON groff mm MACROS

| Action | Macro Name |
|---|---|
| Center justify | .ds C |
| End text box | .b2 |
| Justification off | .sa 0 |
| Justification on | .sa 1 |
| Line fill off | .ds N |
| Line fill on | .ds F |
| New paragraph with x indent | .p x |
| No indents | .ds L |
| Right justify | .ds R |
| Start bold text | .b |
| Start text box | .b1 |
| Use columns | .mc |
| Use one column | .1c |
| Use two columns | .2c |

Some of the more common commands that don't require a macro set are listed in Table 15.3. Experiment with them to see their effect on your documents before printing.

## TABLE 15.3 COMMON groff TYPESETTING COMMANDS

| Action | Command Name |
|---|---|
| Begin new page | .bp |
| Begin new paragraph | .pp |
| Center next x lines | .ce x |
| Center text x | .ce x |
| Insert (space) x inches down | .sp xi |
| Insert x inches down | .sv xi |
| Set font bold | .ft B |
| Set font roman | .ft R |
| Set line spacing to x | .ls x |
| Temporary indent x inches | .ti xi |
| Turn off line fill | .nf |
| Turn on centering | .ce |
| Turn on indenting x inches | .in xi |
| Turn on line fill | .fi |
| Underline next x lines | .ul x |

When you're ready to produce a formatted document, use the groff command's -T command-line option to produce a document in several different document formats. The groff formatter produces PostScript, TeX dvi (discussed next), text, HP printer-control language, or PCL formats. Look at the following example:

```
# groff -Tascii -mm myfile.txt >myfile.txt
# groff -Tps -mm myfile.txt >myfile.ps
# groff -Tdvi -mm myfile.txt >myfile.dvi
```

You can preview these documents before printing by using several different programs, such as gv for PostScript (.ps) or xdvi for dvi files (.dvi).

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_366_0.png)

> The gv program is discussed in Hour 16, “Graphics Tools.”

## Formatting Text with TeX

The TeX typesetting system, originally by Donald E. Knuth, is a collection of programs and other utilities used to produce professionally formatted documents. It is a much more sophisticated system than the groff distribution and includes more than 65 programs, along with such related support files as libraries, macros, fonts, and documentation.

If you install TeX on your system with the lisa or rpm commands, you need at least 30 megabytes for the main distribution, 10 megabytes for a series of related macros called LaTeX, and eight megabytes for 50 different fonts. Obviously, describing the entire system and how to use each different program in the TeX system is beyond this hour. But this section shows you how to get started with a sample document.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_367_0.png)

> Previewing TeX dvi documents requires a preprocessing step that can take several minutes before the pages are even displayed. Files must first be processed by the MakeTeXPK program, and related processes can eat up your system resources. A much better approach is to convert the file to PostScript with the dvips command, found under the /usr/bin directory with the following:
> Now use the gv program with gv tex.ps to read the file.

```
dvips -f < texdoc.dvi >tex.ps
```

You can find documentation for TeX in a variety of places. You can read the manual pages for related files, check the /usr/info directory for TeX information files, and browse to the /usr/TeX/texmf/doc directory. There are 10 different directories of documentation files, but the easiest way to read about your TeX distribution is to use the lynx Web browser with the following:

```
# lynx ls /usr/TeX/texmf/doc/index.html
```

The TeX distribution files are displayed in an organized list that you can browse through to download sample files and guides directly to your home directory. Beginning users should definitely read the TeX Frequently Asked Questions (FAQ) document.

Like the groff program, TeX uses formatting commands inserted in your text files to manipulate how your file looks when printed. You create your file, insert appropriate commands or macros to format text, and then process your document through TeX to create an output file, usually in dvi format, that you can preview or print.

To see a sample of TeX using the LaTeX macros, try processing a sample file in the TeX directories:

```
# latex /usr/TeX/texmf/doc/generic/pstricks/samples.tex
```

This creates a file called samples.dvi. First, convert the file to PostScript with the dvips command, like this:

```
# dvips -f <samples.dvi >samples.ps
```

You see quite a bit of output from this command. When the command finishes, use the gv client to preview the sample.ps document, like so:

```
# gv samples.ps
```

You can use TeX to produce complex diagrams and text, but you have to make the effort to learn TeX first!

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_368_0.png)

> There are many different macros and macro sets included with the TeX formatting system. Covering the details of complex formatting is beyond the scope of this book, but you're encouraged to experiment, starting with simple commands, to get a feel for typesetting documents. There are nearly 100 books about using TeX on the market. If you're serious about learning how to use TeX, a good book is indispensable.

## Printing Text Documents

After you finish formatting your text files, using either a series of filters or inserted typesetting commands, you can print your file to produce a typeset hard copy. To control the printing of your documents, you need to understand how OpenLinux handles printing and how to start, stop, cancel, and control the printing process. There are several printing commands you can use to control the printing process on your system. This section first shows you how your printer is described under OpenLinux and where the important printer files are located. Because most OpenLinux users at home have a parallel printer attached to their computers, this hour's discussion is limited to parallel printers. Printers are known as character mode devices and are listed under the /dev directory. Look at the following example:

```
# ls /dev/lp*
/dev/lp0 /dev/lp1 /dev/lp2
```

This shows the three parallel printer devices that are installed on your system by default.
