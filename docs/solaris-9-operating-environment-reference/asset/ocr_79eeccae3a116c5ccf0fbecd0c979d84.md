# 46

# appcert

This problem is most likely because of static linking of Solaris library that
references that symbol. Because appcert uses the dynamic linker to resolve
symbols, statically linked libraries appear to appcert to be part of the application
code (which, in a sense, they are). This problem can also sometimes happen as
result of macro substitution in a Solaris header file.

To avoid this, whenever possible do not statically link Solaris library
archives into your application.

+   - appcert does not recognize a library as part of Solaris.
Some obsolete Solaris libraries are so old that they were obsolete before their
symbol could be versioned. Consequently, appcert cannot recognize them aseing part of Solaris.

# Options

+   -B
Run in batch mode. When you use this option, the output report
contains one line per binary, beginning with PASS if no problems were
detected for the binary, FAIL if any problems were found, or INC if the
binary could not be completely checked. These labels
to literally. For example, PASS just means that none of the appcert
warnings were triggered. These strings are flush left and can be
selected by grep ^FAIL..., and so forth.

+   - infile
Specify the file infile that contains a list of files (one per line) to
check. This list is appended to the list determined from the
command-line operations.

+   -h
Print the usage information.

+   -L
Prevent appcert from automatically appending shared object
directories to LD_LIBRARY_PATH. By default, appcert examines your
product for the presence of shared objects. If some are found,
appends the directories they reside in LD_LIBRARY_PATH.

+   -S
Append Solaris library directories (that is,
/usr/openwin/lib:/usr/dt/lib to LD_LIBRARY_PATH.

+   - working_dir
Identify the directory in which to run the library components and
create temporary files (default is /tmp).

# Operands

+   {obj | dir}
A complete list of objects or directories that contain the objects
constituting the product to be checked. appcert recursively searches
directories looking for object files; it ignores nonobject files.

# Exit Status

+   0
Run successfully and found no potential binary stability problems.