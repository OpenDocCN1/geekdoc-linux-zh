| String | Package Contains | Example |
|---|---|---|
| `static` | Programs that have been statically linked with certain libraries | `nwutils-static` |
| `devel` | Files required for developing new programs with this system | `slang-devel` |
| `devel-static` | Files required for developing statically linked programs with this system | `slang-devel` |
| `doc` | Regular text documentation | `lilo-doc` |
| `doc-html` | Documentation in HTML format | `povray-doc-html` |
| `doc-<format>` | Documentation in the specified format | `povray-doc-ps` |

Often, software that provides a library to be used by other programs comes as three separate packages:

+   - The main package provides the shared library program binaries use to run.
+   - A development package provides the header files and programming documentation necessary to develop new programs that use the library.
+   - A static development package provides a version of the library that is ready to be statically linked to a new program.

Unless you plan to create or alter programs that use a particular library, you do not need to install the devel packages for that library.

# PACKAGE CONTENTS

To understand how the package manager can support all the tasks listed previously, it is important to know what a package contains.

A binary package contains the following items:

+   - Name and description of the software
+   - Version information
+   - Information about the RPM provider
+   - URL for product home page
+   - Licensing and copyright information
+   - Product classification
+   - Operating system and architecture information
+   - Files and directory information for each file, including names, sizes, permissions, MD5 checksums, symbolic links, file classification (regular, configuration, or documentation), and other information