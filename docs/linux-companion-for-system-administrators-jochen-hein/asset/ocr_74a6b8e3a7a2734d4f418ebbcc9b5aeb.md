# THE REVISION CONTROL SYSTEM (rcs) 339

message, which is also stored. The text file is stored as the difference from the previous version.

Furthermore, the rcs archive contains an access list which can be managed by means of the rcs command. This list specifies which users in the system are allowed to work with this archive and the file contained in it.

# Automatic identification

The rcs can generate special markers in the work file, the so-called rcs markers. To insert such marker into a file, the marker $Id$ can be inserted into the text, for example, into a comment. This marker is replaced by the rcs with '$Id: file name version date status$'.

With this marker on the first page of each module, you can see at which version you are currently working on. The markers are automatically updated by the rcs. To get these marks into the object code of the program too, the ID must be embedded in a string. In the C programming language, for example, this can be shown as in Listing 11.17.

```
static char rcsid[]=
$Id: hello.c,v 1.18 1995/01/15 16:01:00 cschaba Exp$;
```

+   Listing 11.17 Embedding the RCS identification in binary programs.

The ident command extracts this marker from any kind of file, including, for example, object files, binary files, or core dumps. This allows you to find out which versions of modules have been compiled into the program.

It might also be useful to include the marker $Log$ in the source file. This marker collects all log entries that were entered during the storing processes of ci. Thus, the complete version history is stored in the source file as well. A whole series of such markers, which are listed in the man page of the command.

# rcs markers

rcs markers are character strings that begin with the character $, followed by the marker name, followed by, if the marker was already substituted, a colon and the value of the marker, followed by another $. At first, the user will enter the marker without a value; for example $Id$. co recognizes this marker and expands it by co in the work file: