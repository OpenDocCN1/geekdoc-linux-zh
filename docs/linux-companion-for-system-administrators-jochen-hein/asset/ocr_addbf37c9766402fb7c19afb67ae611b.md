# 340 TOOLS (NOT ONLY) FOR PROGRAMMERS

$Author$
The login name of the user who stored the version.

$Date$
The date and time in GMT of the version was stored.

$Header$
A default header which contains the complete rcs file name, the version number, the date, the author's name, the status, and the name of the user who locked the file.

$Id$
A standard header like $Header$, but without specifying the path in the file name.

$Locker$
The login name of the user who locked the version.

$Log$
The log message that can be entered when storing a version. Existing log entries are not removed from the work file; new entries are simply added.

$rcsfile$
The name of the rcs archive.

$Revision$
The version number.

$Source$
The complete pathname of the rcs archive.

$State$
The current status of the version. Default status is 'Exp.' Reasonable status names in program development might be, for example, 'Alpha' or 'Beta'.

After this rather dry introduction, we will look again at an example. Listing 11.18 you will find the header of a file before the rcs markers were expanded. Listing 11.19 shows the same header after rcs has expanded the markers.