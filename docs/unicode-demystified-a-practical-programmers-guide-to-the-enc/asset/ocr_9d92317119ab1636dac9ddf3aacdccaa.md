formats are implementation defined. It is the stated intent of the POSIX.2 commit-tee to define a new archive format in a future revision of the standard. That format will become the default for pax.

The syntax of the pax command is too complex to describe here (as you might expect from looking at all the options available to tar and cpio). If it exists in your system, consult the manual pages. The USENIX Association funded the develop-ment of a portable implementation of pax and placed it in the public domain, so this utility is now widely available. Refer to the pax man page for more informa-tion.

# printf

The printf utility was invented largely to deal with the incompatibility between the BSD and System V versions of echo (page 1157). BSD echo treats a first argument of -n in a special fashion, whereas System V will echo. System V echo treats certain strings starting with \ in a special fashion, whereas BSD will echo. POSIX.2 states that any echo command line in where -n is the first argument or in which any argument starts with \ will have implementation-defined behavior. To print any but the simplest strings, you should use printf.

The f in printf stands for formatted, and the printf utility allows you to print strings to standard output under the control of a formatting argument. The syntax is

```
printf format [string ...]
```

Both the name printf and the syntax of the format string are borrowed from C. Refer to the printf man page for more information.

# The User Portability Utilities Option (UPE)

The UPE is a collection of 37 utilities and shell built-in commands for interactive use. This portion of the standard is an option; that is, a system can conform to POSIX.2 without providing these. Their purpose is to promote user portability by creating a uniform interactive command environment. Following is a list of the UPE utilities. Those that are not described in the main part of this text are marked with an asterisk (*).

| alias | at | batch* | bg | crontab |
| csplit* | ctags* | df | du | ex |