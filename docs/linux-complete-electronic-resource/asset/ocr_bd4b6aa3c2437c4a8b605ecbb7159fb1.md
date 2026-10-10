# INTRODUCTION

Mtools is a public domain collection of tools to allow Unix systems to manipulate MS-DOS files: read, write, and move around files on an MS-DOS filesystem (typically a floppy disk). Where reasonable, each program attempts to emulate the MS-DOS equivalent command. However, unnecessary restrictions and oddities of DOS are not emulated. For instance, it is possible to move subdirectories from one subdirectory to another.

# COMMON FEATURES OF ALL MTOOLS COMMANDS

# OPTIONS AND FILENAMES

MS-DOS filenames are composed of a drive letter followed by a colon, a subdirectory, and a filename. Only the filename part is mandatory, the drive letter and the subdirectory are optional. Filenames without a drive letter refer to Unix files. Subdirectory names can use either the / or ` separator. The use of the ` separator or wildcards requires the names to be enclosed in quotes to protect them from the shell. However, wildcards in Unix filenames should not be enclosed in quotes, because here we *want* the shell to expand them. The regular expression “pattern matching” routines follow the Unix-style rules. For example, * matches all MS-DOS files in lieu of * . The archive, hidden, read-only and system attribute bits are ignored during pattern matching.

All options use the - (minus) as their first character, not / as you'd expect in MS-DOS.

Most mtools commands allow multiple filename parameters, which doesn't follow MS-DOS conventions, but which is more user-friendly.

Most mtools commands allow options that instruct them how to handle file name clashes. See section name clashes, for more details on these. All commands accept the -V flags which print the version, and most accept the -v flag, which switches on verbose mode. In verbose mode, these commands print out the name of the MS-DOS files upon which they act, unless stated otherwise. See section “Commands,” for a description of the options which are specific to each command.

# DRIVE LETTERS

The meaning of the drive letters depends on the target architectures. However, on most target architectures, drive A is the first floppy drive, drive B is the second floppy drive (if available), drive J