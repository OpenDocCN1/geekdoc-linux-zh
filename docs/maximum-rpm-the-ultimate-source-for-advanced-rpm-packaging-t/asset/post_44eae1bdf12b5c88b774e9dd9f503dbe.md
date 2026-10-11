
## The ROOT Tag

The ROOT tag is not available for use with --queryformat.

## The FILEUSERNAME Tag

The FILEUSERNAME tag is used to display the owner, in alphanumeric form, of each of the files that comprise the package.

Array: No

Used with modifiers: N/A

## The FILEGROUPNAME Tag

The FILEGROUPNAME tag is used to display the group, in alphanumeric form, of each of the files that comprise the package.

Array: Yes (Size: One entry per file)

Used with modifiers: N/A

## The EXCLUDE Tag

The EXCLUDE tag is deprecated and should no longer be used.

## The EXCLUSIVE Tag

The EXCLUSIVE tag is deprecated and should no longer be used.

## The ICON Tag

The ICON tag is not available for use with --queryformat.

## The SOURCERPM Tag

The SOURCERPM tag is used to display the name of the source package from which this binary package was built.

Array: No

Used with modifiers: N/A

## The FILEVERIFYFLAGS Tag

The FILEVERIFYFLAGS tag is used to display the numeric value of the file verification flags for each of the files that comprise the package.

Array: Yes (Size: One entry per file)

Used with modifiers: N/A

Since there is no modifier to display the verification flags in human-readable form, it will be necessary to manually interpret the flag values based on the RPMVERIFY_\_xxx #defines contained in `rpm1.h`. This file is part of the `rpm-devel` package and is also present in the RPM source package.

## The ARCHIVESIZE Tag

The ARCHIVESIZE tag is used to display the size, in bytes, of the archive portion of the original package file.

Array: No

Used with modifiers: N/A

## The PROVIDES Tag

The PROVIDES tag is used to display the capabilities the package provides.

Array: Yes (Size: One entry per provide)

Used with modifiers: N/A

## The REQUIREFLAGS Tag

The REQUIREFLAGS tag is used to display the requirement flags for each capability the package requires.

Array: Yes (Size: One entry per require)

Used with modifiers: `:depflags`

## The REQUIRENAME Tag

The REQUIRENAME tag is used to display the capabilities the package requires.

Array: Yes (Size: One entry per require)

Used with modifiers: N/A

## The REQUIREVERSION Tag

The REQUIREVERSION tag is used to display the version-related aspect of each capability the package requires.

Array: Yes (Size: One entry per require)

Used with modifiers: N/A

## The NOSOURCE Tag

The NOSOURCE tag is used to display the source archives that are not contained in the source package file.

Array: Yes (Size: One entry per nosource)

Used with modifiers: N/A

## The NOPATCH Tag

The NOPATCH tag is used to display the patch files that are not contained in the source package file.

Array: Yes (Size: One entry per nopatch)

Used with modifiers: N/A

## The CONFLICTFLAGS Tag

The CONFLICTFLAGS tag is used to display the conflict flags for each capability the package conflicts with.

Array: Yes (Size: One entry per conflict)

Used with modifiers: `:depflags`

## The CONFLICTNAME Tag

The CONFLICTNAME tag is used to display the capabilities that the package conflicts with.

Array: Yes (Size: One entry per conflict)

Used with modifiers: N/A

## The CONFLICTVERSION Tag

The CONFLICTVERSION tag is used to display the version-related aspect of each capability the package conflicts with.

Array: Yes (Size: One entry per conflict)

Used with modifiers: N/A

## The DEFAULTPREFIX Tag

The DEFAULTPREFIX tag is used to display the path that will, by default, be used to install a relocatable package.

Array: No

Used with modifiers: N/A

## The BUILDFROOT Tag

The BUILDFROOT tag is not available for use with --queryformat.

## The INSTALLPREFIX Tag

The INSTALLPREFIX tag is used to display the actual path used when a relocatable package was installed.

Array: No

Used with modifiers: N/A

## The EXCLUDEARCH Tag

The EXCLUDEARCH tag is used to display the architectures that should not install this package.

Array: Yes (Size: One entry per excludearch)

Used with modifiers: N/A

## The EXCLUDEOS Tag

The EXCLUDEOS tag is used to display the operating systems that should not install this package.

Array: Yes (Size: One entry per excludeos)

Used with modifiers: N/A

## The EXCLUSIVEARCH Tag

The EXCLUSIVEARCH tag is used to display the architectures that are the only ones that should install this package.

Array: Yes (Size: One entry per exclusivearch)

Used with modifiers: N/A

## The EXCLUSIVEOS Tag

The EXCLUSIVEOS tag is used to display the operating systems that are the only ones that should install this package.

Array: Yes (Size: One entry per exclusiveos)

Used with modifiers: N/A

## The AUTOREPROV Tag

The AUTOREPROV tag is not available for use with --queryformat.

## The RPMSVERSION Tag

The RPMSVERSION tag is used to display the version of RPM that was used to build the package.

Array: No

Used with modifiers: N/A

## The TRIGGERSCRIPTS Tag

The TRIGGERSCRIPTS tag is reserved for a future version of RPM.

## The TRIGGERNAME Tag

The TRIGGERNAME tag is reserved for a future version of RPM.

## The TRIGGERVERSION Tag

The TRIGGERVERSION tag is reserved for a future version of RPM.

## The TRIGGERFLAGS Tag

The TRIGGERFLAGS tag is reserved for a future version of RPM.

## The TRIGGERINDEX Tag

The TRIGGERINDEX tag is reserved for a future version of RPM.

## The VERIFYSRIPT Tag

The VERIFYSRIPT tag is used to display the script to be used for package verification.

Array: No

Used with modifiers: N/A

# Concise Spec File Reference

## E.1. Comments

Comments are a way to make RPM ignore a line in the spec file. To create a comment, enter a pound sign (#) at the start of the line. Any text following the comment character will be ignored by RPM:

```
# This is the spec file for playmidi 2.3...
```

Comments can be placed in any section of the spec file.

For more information, see section 13.1 in Chapter 13, “Inside the Spec File.”

## E.2. The Preamble

The preamble contains information that will be displayed when users request information about the package.

### E.2.1. Package-Naming Tags

Package-naming tags are used to define the parts of the package’s label. For more information about these tags, see section 13.2.1.

#### E.2.1.1. The name Tag

The name tag is used to define the name of the software being packaged:

Name: cdplayer

#### E.2.1.2. The version Tag

The version tag defines the version of the software being packaged:

Version: 1.2

#### E.2.1.3. The release Tag

The release tag can be thought of as the package’s version:

Release: 5

### E.2.2. Descriptive Tags

Descriptive tags are used to define various types of information about the package. For more information about these tags, see section 13.2.2.

#### E.2.2.1. The %description Tag

The %description tag is used to define an in-depth description of the packaged software. In the descriptive text, a space in the first column indicates that that line of text should be presented to users as is, with no formatting done by RPM. Blank lines in the descriptive text denote paragraphs:

```
%description
 It slices!
 It dices!
 It's a CD player app that can't be beat.
 
By using the resonant frequency of the CD itself, it is able to simulate
20X oversampling. This leads to sound quality that cannot be equaled with
more mundane software...
```

You can make the %description tag specific to a particular subpackage by adding the subpackage name and, optionally, the -n option:

```
%description bar
 
%description -n bar
```

The subpackage name and the usage of the -n option must match those defined with the %package directive.

#### E.2.2.2. The summary Tag

The summary tag is used to define a one-line description of the packaged software:

```
Summary: A CD player app that rocks!
```

#### E.2.2.3. The copyright Tag

The copyright tag is used to define the copyright terms applicable to the software being packaged:

```
Copyright: GPL
```

#### E.2.2.4. The distribution Tag

The distribution tag is used to define a group of packages of which this package is a part:

```
Distribution: Doors '95
```

#### E.2.2.5. The icon Tag

The icon tag is used to name a file containing an icon representing the packaged software:

```
Icon: foo.xpm
```

The file may be in either GIF or XPM format, although XPM is preferred. In either case, the background of the icon should be transparent.
