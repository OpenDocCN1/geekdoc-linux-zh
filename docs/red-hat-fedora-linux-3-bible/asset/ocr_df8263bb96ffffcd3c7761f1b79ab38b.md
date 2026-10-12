# Creating a man page with *Groff*

Before HOW-TOs and info files, man pages were the foundation for information about UNIX and UNIX-like systems. Each command, file format, device, or other component either had its own man page or was grouped on a man page with similar components. To create your own man page requires that you learn a few macros (in particular, man macros). Figure 6-3 shows the source for a fictitious man page for a command called waycool.

> **TIP:** Most man pages are stored in subdirectories of `/usr/share/man`. Before you create a man page, refer to similar man pages to see the markup and headings they include. In man7 you can find; man2 has system calls; man3 has library functions; man4 has special device files (`/dev/*`); man5 has file formats; man6 has games; man7 has miscellaneous components; and man8 has administrative commands.

A few other kinds of macros are used in the man page. The IP macros format indented paragraphs for things such as options. The man page also contains some lower-level font requests; for example, `\fB` says to change the current font to bold, `\fI` changes the font to italic, and `\fR` changes it back to regular. (This markup is better asking for a particular font type because it just changes to bold, italic, or regular for the current font.) Figure 6-4 shows what the waycool man page looks like after it is formatted with *groff*:

```
`$ groff -man -Tps -1 waycool.1`
```
."     " waycool.1 - the groff document processor source for the waycool command
."     .   " .TH WAYCOOL 1 "May 12, 2002" GBD "Linux Programmer's Manual"
.   B NAME
waycool - a way cool command
.   B SYNOPSIS
./libgswaycool/ V1 ./lib/waycool V1 \fIf file ...\fR
.   B VERCION
This man page documents the GBD waycool_version X.X.
.   B DESCRIPTION
Vlibgswaycool/V1 is a way cool command.
.   IP
THIS version of \fBlibgswaycool/V1\fR is better than the last one.
.   B OPTIONS
.   IP .ui
See all options with it.
.   IP .ui
Run nonewaycool.
.   B FILES
.   P
/fct/ waycool links instead of my referenced file
(failable only on systems that can change the
appearance of a gwdlin)
.   P
Print the version number with the command.
.   B ENVIRONMENT
.   IP
If you don't like the command, don't tell me. It will just hurt my feelings.
.   B ENVIRONMENT VARIABLES
.   IP
These environment variables are used by \fBlibgswaycool/V1\fR:
.   IP \"WAYCOOL" "V1
This sets the GBDsway version.
.   IP \"WAYCOOL" "V2
This contains the location of the waycool database.
.   B FILES
`/etc/gswaycool` - Directory containing waycool stuff.
.   B SEE ALSO
GDB `Groff` documentation:\`/gsw/groff`
See ``"WAYCOOL" `MAN`
Report bugs to GDB `libgswaycool/gsw.org`.
.   B COPYRIGHT
Copyright Xcon 2002 Free Software Foundation, Inc.
.   IP
This is free software; see the source for exacting conditions. There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
.   B REFERENCES
I'd like to thank all my friends.
```
```
```
```

**Figure 6-3:** Simple markup is required to create man pages.