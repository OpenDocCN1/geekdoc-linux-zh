# zip, zipcloak, zipnote, zipsplit 1587

-T  Test the integrity of the new zipfile. If the check fails, the old zipfile
unchanged and (with the -m option) no input files are removed.

-u
Replace (update) an existing entry in the zip archive only if it has been
modified more recently than the version already in the zip archive.
The following example adds new files in the current directory and
updates any files modified since the archive stuff. zip was last created
or modified. Note that zip does not try to pack stuff. zip into itself.

zip -u stuff *
Note that the -u option with no arguments acts like the -f (fhen)
option.

-v
Verbose mode or print diagnostic information. Normally, when
applied to real operations, this option enables the display of a progress
indicator during compression and requests verbose diagnostic
information about zipfile oddities.

Print a diagnostic screen when -w is the only command-argument
and standard output is not redirected to a file. In addition to the help
screen with program name, version, and release date, some
pointers to the Info-ZIP home name and distribution sites are displayed.
The option shows information about the target environment (compiler type
and OS, version, compilation date, and the enabled optional
features used to create the zip executable.

-v
[VMS] Save VMS file attributes. zip archives created with this option
gener cannot be used by other systems.

-w
[VMS] Append the version number of the files to the name, including
multiple versions of files. (Default: use only the most recent version of
a specified file.)

-x files
Explicitly exclude the specified files. The following example includes
the contents of foo in foo zip while excluding all the files that end in
o.. The backslash allows the file-name substitution, so the name
matching is performed by zip at all directory levels.

```
zip -r foo -x *
```

Another use of this option is shown in the following example, which
includes the contents of foo in foo zip while excluding all the files
that match the patterns in the file exclude.

```
zip -r foo -x@exclude.lst
```

-X
Do not save extra file attributes (Extended Attributes on OS/2,
UID/GID and file times on UNIX).

-y
Store symbolic links as symbolic links in the zip archive, instead
ofcompressing and storing the file referred to by the link (ZIP only).

-z
Prompt for a multiline comment for the entire zip archive. End the
comment with a line containing either a period or an end-of-file
condition (^D on UNIX; ^Z on MS-DOS, OS/2, and VAXMS). You can
take the comment from a file, as shown in the following example.