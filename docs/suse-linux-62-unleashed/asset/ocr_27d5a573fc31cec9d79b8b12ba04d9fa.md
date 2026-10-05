# Support for Misc Binaries

Long before operating systems provided for running Java applications from the command line, binary executable support for Class files was added to the Linux kernel. Later, this feature was generalized to all binary and interpreter types. Using the sysctl pseudo-files, Linux will integrate Java, MS-DOS programs, Windows programs, tk/tcl, Perl, or any other strange executable as seamlessly as an ELF binary or a shell script.

To use the misc binaries support, you need to register the *magic cookie* of the file type and the corresponding interpreter through the sysctl pseudo-files in `/proc/sys/fs/binfmt_misc`. You can derive the magic cookie from the first few bytes of the file or the filename (such as `.com` or `.exe`), and you can register it by echoing a string to `/proc/sys/fs/binfmt_misc/register`, where the format of the string specifies the following:
`name:type:offset:magic:mask:interpreter`

+   - name is an arbitrary identifier for this executable type.
- type specifies M or E, depending on whether the cookie is mask or extension.
- offset is the count in bytes from the front of the file. If omitted, a default of 0 is used.
- magic is the sequence of bytes to match. Hex codes may be specified as `\xA0` or `\xFF` (be careful to escape the slash character if you set the magic through a shell