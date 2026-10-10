
## Chapter 6: Publishing with Fedora and RHEL

Groff macro packages are stored in `/usr/share/groff/*/mac`. The man macros are called from the `an.tmac` file, mm macros are from `m.tmac`, and me macros are from `e.tmac`. The naming convention for each macro package is `xxx.tmac`, where xxx is replaced by one or more letters representing the macro package. In each case, you can understand the name of the macro package by adding an m to the beginning of the file suffix.

> **TIP:** Instead of noting a specific macro package, you can use `-mandoc` to choose a macro package.

When you run the groff formatting command, you can indicate on the command line which macro packages you are using. You can also indicate that the document should be run through any of the following commands that preprocess text for special formats:

- eqn — This preprocessor formats macros that produce equations in groff.
- pic — This preprocessor formats macros that create simple line drawings in groff.
- tbl — This preprocessor formats macros that produce tables within groff.

The formatted Groff document is output for a particular device type. The device can be a printer, a window, or (for plain text) your shell. Here are output forms supported by Groff:

- ps — Produces PostScript output for a PostScript printer or a PostScript previewer.
- lj4 — Produces output for an HP LaserJet4 printer or other PCL5-compatible printer.
- ascii — Produces plain-text output that can be viewed from a Terminal window.
- dvi — Produces output in TeX dvi, to output to a variety of devices described later.
- X75 — Produces output for an X11 75 dots/inch previewer.
- X100 — Produces output for an X11 100 dots/inch previewer.
- latin1 — Produces typewriter-like output using the ISO Latin-1 character set.

### Formatting and printing documents with Groff

You can try formatting and printing an existing Groff document using any man pages on your Fedora or RHEL system (such as those in `/usr/share/man/*`). (Those man pages are compressed, so you can copy them to a temporary directory and unzip them to try out Groff.)

These commands copy the chown man page to the `/tmp` directory and unzips it. Then, groff formats the chown man page in plain text so you can page through it on your screen.

```bash
$ cp /usr/share/man/man1/chown.1.gz /tmp
$ gunzip /tmp/chown.1.gz
$ groff -Tascii -man /tmp/chown.1 | less
```

In the previous example, the chown man page (`chown.1.gz`) is copied to the `/tmp` directory, is unzipped (using gunzip), and is output in plain text (`-Tascii`) using the man macros (`-man`). The output is piped to `less`, to page through it on your screen. Instead of piping to `less` (`| less`), you can direct the output to a file (`>/tmp/chown.txt`).

To format a man page for typesetting, you can specify PostScript or HP LaserJet output. You should either direct the output to a file or to a printer. Here are a couple of examples:

```bash
$ groff -Tps -man /tmp/chown.1 > /tmp/chown.ps
$ groff -Tlj4 -man -1 /tmp/chown.1
```

The first example creates PostScript output (`-Tps`) and directs it to a file called `/tmp/chown.ps`. That file can be read by a PostScript previewer (such as Ghostscript) or sent to a printer (`lpr /tmp/chown.ps`). The next example creates HP LaserJet output (`-Tlj4`) and directs it to the default printer (`-1` option).

> **TIP:** Using `man2html`, you can convert man pages to HTML format for display in a browser. For example: `zcat /usr/share/man/man1/chown.1.gz | man2html > /tmp/chown.htm`.

### Creating a man page with Groff

Before HOW-TOs and info files, man pages were the foundation for information about UNIX (and UNIX-like) systems. Each command, file format, device, or other component either had its own man page or was grouped on a man page with similar components. Creating your own man page requires that you learn a few macros (in particular, man macros). Figure 6-3 shows the source for a fictitious man page for a command called `waycool`.

> **TIP:** Most man pages are stored in subdirectories of `/usr/share/man`. Before you create a man page, refer to similar man pages to see the markup and the headings they include. In `man1` are commands; `man2` has system calls; `man3` has library functions; `man4` has special device files (`/dev/*`); `man5` has file formats; `man6` has games; `man7` has miscellaneous components; and `man8` has administrative commands.

A few other kinds of macros are used in the man page. The `.IP` macros format indented paragraphs for things such as options. The man page also contains some lower-level font requests; for example, `.B` says to change the current font to bold, `.I` changes the font to italic, and `.R` changes it back to regular font. (This markup is better than asking for a particular font type because it just changes to bold, italic, or regular for the current font.) Figure 6-4 shows what the `waycool` man page looks like after it is formatted with groff:

```bash
$ groff -man -Tps -1 waycool.1
```

```
.\" sgsconf.1 - the sgsconf document processor source for the sgsconf command
.\"
.TH sgsconf 1 "Sept 12, 2005" GHI "Linux Programmer's Manual"
.SH NAME
sgsconf \- my cool command
.SH SYNOPSIS
.B sgsconf
.BR [ \fB\-W\fR abca] [ \fB\-i\fR file ... ]
.SH VERSION
This man page documents the GHI sgsconf version 1.0
.SH DESCRIPTION
.B sgsconf
 is a very cool command.

This version of .BR sgsconf is better than the last one.
.SH OPTIONS
.TP
.B \-P N
Run all options with it.
.TP
.BR A "Run sane options."
.TP
.BR \-P =
affect symbolic links instead of any referenced file
(bash only) only on options that can change the
ownership of a symbolic link
.TP
.BR \-P =
Print the version number with the command.
.SH COMMENTS
if you don't like the command, don't tell me, it will just hurt my feelings.
.SH "ENVIRONMENT VARIABLES"
These environment variables are used by .BR sgsconf:
.TP
.BR "F" "W" "F" "A" "D" "F" "T"
This sets the # Display variable.
.TP
.BR "NOTICE" "\
This contains the location of the sgsconf database.
.SH FILES
./usr/cs/sgsconf - Directory containing sgsconf stuff.
.SH AUTHOR
DeB is GHI, colie: gsgconf@sorg, com
.SH "COPYING RIGHTS"
.B sgsconf belongs to GHI: [sgsconf@ghs.org].
.SH COPYRIGHT
Copyright © 2005 free software foundation, inc.
the
This is free software; see the source for copying conditions. There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
.SH ACKNOWLEDGEMENTS
I'd like to thank all my friends.
```

Figure 6-3: Simple markup is required to create man pages.

![](img/fb202c163797a743c3c6cf236316bc96_296_0.png)

Figure 6-4: Man page formatting adds headers and lays out the page of text.

Table 6-1 lists the macros that you can use on your man pages. These macros are described on the `man(7)` manual page (type `man 7 man` to view that page).

### Table 6-1: man Macros

| Macro | Description |
|---|---|
| .B | Bold. |
| .BI | Bold, then italics (alternating). |
| .BR | Bold, then Roman (alternating). |
| .DT | Set default tabs. |
| .HP | Begin a hanging indent. |
| .I | Italics. |
| .IB | Italics, then bold (alternating). |
| .IP | Begin hanging tag. For options. Long tags use .TP. |
| .IR | Italics, then Roman (alternating). |
| .LP | Begin paragraph. |
| .PD | Set distance between paragraphs. |
| .PP | Begin paragraph. |
| .RB | Roman, then bold (alternating). |
| .RE | End relative indent (after .RS). |
| .RI | Roman, then italics (alternating). |
| .RS | Begin relative indent (use .RE to end indent). |
| .SB | Small text, then bold (alternating). |
| .SM | Small text. Used to show words in all caps. |
| .SH | Section head. |
| .SS | Subheading within a .SH heading. |
| .TH | Title heading. Used once at the beginning of the man page. |
| .TP | Begin a hanging tag. Begins text on next line, not same line as tag. |

### Creating a letter, memo, or white paper with Groff

Memorandum macros (which are used with the `-mm` option of Groff) were once popular among UNIX users for producing technical documents, letters, and memos. Although more modern word processors with a variety of WYSIWYG templates have made mm outdated, in a pinch mm can still be a quick way to create a typeset-style document in a text environment.
