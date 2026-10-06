# Chapter 6: Publishing with Fedora and RHEL 259

> TIP: Most man pages are stored in subdirectories of /usr/share/man. Before you create a page, refer to similar man pages to see the markup and the headers include: man1 are commands; man2 has system calls; man3 has library functions; man4 has device files (/dev/*); man5 has file formats; man6 has games; man7 has miscellaneous components; and man8 has administrative commands.

A few other macros are used in the man page. The IP macros format identifies paragraphs for things using offsets. The man page also contains lower-level requests, for example, \B to change the current font to bold, \I to change the font to italic, and \R changes back to regular font. (This is better than asking for a particular font because it just changes to bold, italic, or regular for the current font.) Figure 6-4 shows how the weeway man page looks after it is formatted with groff:

```
$ groff -man -Tps -1 weeway,1
```

| weeway(1) Linux Programmer's Manual | weeway(1) |
| NAME weeway - my command. |
| SYNTAX weeway [option] [file], ... |
| VERSION This page does not contain the GNU man page version X.XX. |
| DESCRIPTION weeway is a cool command. This version of weeway is better than the last one. |
| OPTIONS -B font in bold.\\n-I font in italic.\\n-U offset text in underline of any reference text (available only on systems that support the selection of text).\n-t Print the version number with the command. |
| COMMENTS If you don't call the command, it won't work. It will just hurt your feelings. |
| ENVIRONMENT These variables are used by weeway:\nDISPLAY This sets the Display variable.\nWAYPATH This contains the location of the weeway database. |
| FILES weeway - Directory containing weeway stuff. |
| AUTHOR You contact <author@example.com> |
| REPORTING Report bugs to <bug@fedora.org> |
| COPYRIGHT © 20XX Free Software Foundation, Inc.
You may distribute and modify text under the following conditions: There is NO WARRANTY, except as specified HERE. WRITTEN FOR A PARTICULAR PURPOSE. |
| ACKNOWLEDGEMENTS This is not without any forwards. |

Figure 6-4: Man formatting adding headers and lays out the page of text.

Macros are described on the man(7) man page (**type man 7 man** to view that page).

# Text processing with TeX/LaTeX

TeX (pronounced "tex") is a collection of commands used primarily to produce scientific and mathematical typeset documents. The most common way to use TeX is by calling a macro package. The most popular macro package for Tex is LaTeX, which takes a higher-level