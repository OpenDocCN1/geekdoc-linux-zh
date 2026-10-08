# ctags

# 225

+   -x    Produce a list of object names, the line number, and file name on which each is defined, as well as the text of that line and print it on the standard output. This list provides a simple index that can be printed as an off-line readable function index.

# Operands

+   -file.c    Treat files with basenames ending with the .c suffix as C-language source code.

+   -file.h    Treat files with basenames ending with the .h suffix as C-language source header files.

+   -file.f    Treat files with basenames ending with the .f suffix as FORTRAN-language source code.

# Usage

The -v option is used mainly with vgrind, which is part of the optional BSD Compatibility package.

# Notes

Recognition of functions, subroutines, and procedures for FORTRAN and Pascal is done in a simple-minded way. No attempt is made to deal with block structure; if you have two Pascal procedures in different blocks with the same name, you lose.

The method of deciding whether to look for C or Pascal and FORTRAN functions is a hack.

The ctags command does not know about #ifdefs.ctags command should know about Pascal types. It relies on the input being used to detect typedefs. of -tx shows only the last line of typedefs.

# Examples

Using ctags with the -v option produces entries in an order that may not be appropriate for vgrind. To produce results in alphabetical order, you may want to pipe the output through sort -f, as shown in the following example

```
ctags -v ctags filename.h | sort -f > index
```

```
ctags% vgrind -x index
```

To build a tags file for C sources in a directory hierarchy rooted at sourdir, create an empty tags file, then run find(1), as shown in the following example

```
ctags$ cd sourdir; rm -f tags; touch tags
```

```
ctags$ find . \ -name SCCS -prune -name '*.c' -o -name '*.h' \ -exec
ctags -u ( \;
```

> Note — Spaces must be entered exactly as shown.

# Environment Variables

See environ(5) for descriptions of the following environment variables that affect the execution of ctags: LC_COLLATE, LC_CTYPE, LC_MESSAGES, and NLPATH.