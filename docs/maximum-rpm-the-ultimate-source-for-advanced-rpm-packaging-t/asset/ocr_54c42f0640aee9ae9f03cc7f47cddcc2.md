# The ROOT Tag

The ROOT tag is not available for use with --queryformat.

# The FILEUSERNAME Tag

The FILEUSERNAME tag is used to display the owner, in alphanumeric form, of each of the files that comprise the package.

Array: No

Used with modifiers: N/A

# The FILEGROUPNAME Tag

The FILEGROUPNAME tag is used to display the group, in alphanumeric form, of each of the files that comprise the package.

Array: Yes (Size: One entry per file)

Used with modifiers: N/A

# The EXCLUDE Tag

The EXCLUDE tag is deprecated and should no longer be used.

# The EXCLUSIVE Tag

The EXCLUSIVE tag is deprecated and should no longer be used.

# The ICON Tag

The ICON tag is not available for use with --queryformat.

# The SOURCERPM Tag

The SOURCERPM tag is used to display the name of the source package from which this binary package was built.

Array: No

Used with modifiers: N/A

# The FILEVERIFYFLAGS Tag

The FILEVERIFYFLAGS tag is used to display the numeric value of the file verification flags for each of the files that comprise the package.

Array: Yes (Size: One entry per file)

Used with modifiers: N/A

Since there is no modifier to display the verification flags in human-readable form, it will be necessary to manually interpret the flag values based on the RPMVERIFY_\_xxx #defines contained in `rpm1.h`. This file is part of the `rpm-devel` package and is also present in the RPM source package.