# pathchk 1025

portable (that is, no file-name truncation results). More extensive portability checks are provided by the -p option.

By default, pathchk checks each component of each path operand based on the underlying file system. A diagnostic is written for each path operand that:

+   - Is longer than PATH_MAX bytes.
- Contains any component longer than NAME_MAX bytes in its containing directory.
- Contains any component in a directory that is not searchable.
- Contains any character in any component that is not valid in its containing directory.

The format of the diagnostic message is not specified but indicates the error detected and the corresponding path operand.

It is not considered an error if one or more components of a path operand do not exist as long as a file matches the path name specified by the missing components could be created and such a file does not violate any of the checks specified.

# Options

+   -p Instead performing checks based on the underlying file system, a diagnostic for each path operand that:

+   - Is longer than _POSIX_PATH_MAX bytes.
- Contains any component longer than _POSIX_NAME_MAX bytes.
- Contains any character in any component that is not in the portable file-name character set.

# Operands

+   path A path to be checked.

# Usage

largefile(5) for the description of the behavior of pathchk when encountering greater than or equal to 2 Gbytes (2**31 bytes).

# Examples

The following example verifies that all paths in an imported data interchange archive are legitimate and unambiguous on the current system.

```
pax -f archive | sed -e ' // .*/s/// | xargs pathchk
if [ $ -eq 0 ];
then
    path -r -f archive
else
    echo Investigate problems before importing files.
fi
```

This example verifies that all files in the current directory hierarchy could be moved to any system conforming to the X/Open specification that also supports the path(1) command.

```
find .print | xargs pathchk -p
if [ $ -eq 0 ];
```