the only way to bring order is through documentation. Linux has tons of it—if you know where to look.

Linux is a fairly “standard” UNIX as unices go. There are several generic UNIX books that can help you with additional depth and more advanced topics. A list of recommended readings is included at the end of this chapter. Also, if you have access to the Internet, there are several valuable sources of information that you can tap into, including mailing lists and Usenet news groups. Knowing how to use them properly will help you get the answers you need.

# UNIX Manual Pages

Your first stop for information is the UNIX man pages. If you are having trouble with a command or some other tool in the system, it is very likely that the tool comes with documentation in the form of a man page. A man page is the standard UNIX online documentation format used by the man program.

The UNIX manual is slowly becoming a dinosaur, because better programs exist for reading documentation. The one positive thing about the UNIX manual is that it exists in all unices, Linux or otherwise. For this reason, it’s important that you learn how to use it properly.

To read the UNIX manual, you use the man command, and as an argument you give it the name of a program you want to know something about. The following example shows a section of what man prints out if you ask for information about the bash shell:

```
[alberto@digital alberto]$ man bash
BASH(1)                                                                 BASH(1)

NAME
    bash - GNU Bourne-Again Shell

SYNOPSIS
    bash [options] [file]

COPYRIGHT
    Bash is Copyright (c) 1989, 1991 by the Free Software Foundation, Inc.

DESCRIPTION
    Bash is an sh-compatible command language interpreter that executes commands read from the standard input or from a file. Bash also incorporates useful features from the Korn and C shells (ksh and csh).

    Bash is ultimately intended to be a conformant implementation of the IEEE Posix Shell and Tools specification (IEEE Working Group 1003.2).
:
```

As you can see, the man command provides a formatted version of the online manual. The colon (:) at the end of the listing indicates that there’s more information. Man information is passed through a pager program called less. You may recall that less displays information one screenful at a time. Here are a few things you can do with less:

+   - Press the Spacebar to view the next page.
+   - Type /word where word is a term that you are looking for. This will search the document for the word you specify and stop the pager at word’s first occurrence.
+   - Type q to return to the command prompt.

Try the man command to read some information about the man command (man man).