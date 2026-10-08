# lint — C Program Verifier

Synopsis
/usr/ucb/bin/lint [options]

Description
Use the lint command to detect portability problems, bugs, the BSD, and other potential errors in C programs. /usr/ucb/bin/lint is the interface to the link/ccs Compatibility Package C program verifier. It is a script that lists for /usr/ccs/bin/ucblint to the C program verifier. /usr/ccs/bin/ucblint is available only with the SPROcc package, whose default location is /opt/SDN/mspro. /usr/ucb/lint is identical to /usr/ccs/bin/ucblint, except BSD headers and BSD libraries are linked before base libraries. The man/lint.1 manual page is available only with the SPROcc package.

Options
/usr/ucb/lint accepts the same options as /usr/ccs/bin/ucblint, with the following exceptions.

+   -Idir Search for included files that do not begin with a slash (/) before searching the usual directories. Search the directories for -I options in the order specified. The preprocessor searches for #include files in the directory containing a source file, and then in directories with -i options (if any), then /usr/ucblintinclude, and finally, /usr/include.

+   -Ldir Add to the list of directories searched for libraries by /usr/ccs/bin/ucblint. This option is passed to /usr/ccs/bin/ld. Directories specified with this option are searched before /usr/uclib and /usr/lib.

+   -YP, dir Change the default directory used for finding libraries.

Exit Status
0 Successful completion.
>0 An error occurred.

Files
/usr/lint/bin/ld Link editor.
/usr/lib/libc C library.
/usr/ucblinclude BSD compatibility directory for header files.
/usr/ucblib BSD compatibility directory for libraries.