# E.7. The `%package` Directive

The `%package` directive is used to control the creation of subpackages. The subpackage name is derived from the first `name` tag in the spec file, followed by the name specified after the `%package` directive. Therefore, if the first `name` tag is

Name: foo

and a subpackage is defined with the following `%package` directive:

%package bar

the subpackage name will be foo-bar.

For more information on this package and its options, see section 13.7 in Chapter 13.

# E.7.1. The `%package -n` Option

The `-n` option is used to change how RPM derives the subpackage name. When the `-n` option is used, the name following the `%package` directive becomes the complete subpackage name. Therefore, if a subpackage is defined with the following `%package` directive:

%package -n bar

the subpackage name will be bar.

# E.8. Conditionals

The `%ifxxx` conditionals are used to begin a section of the spec file that is specific to a particular architecture or operating system. They are followed by one or more architecture or operating system specifiers, each separated by commas or whitespace.

Conditionals may be nested within other conditionals, provided that the inner conditional is completely enclosed by the outer conditional. For more information about conditionals, see section 13.8 in Chapter 13.

# E.8.1. The `%ifarch` Conditional

If the build system’s architecture is specified, the part of the spec file following the `%ifarch` but before an `%else` or `%endif` will be used during the build:

%ifarch i386 sparc