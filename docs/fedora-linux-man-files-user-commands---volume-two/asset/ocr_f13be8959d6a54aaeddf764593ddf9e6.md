# GNU EXTENSIONS

Gawk has a too-large number of extensions to POSIX awk. They are described in this section. All the extensions described here can be disabled by invoking gawk with the —traditional or —posix options.

The following features of gawk are not available in POSIX awk.

No path search is performed for files named via the -f option. Therefore the AWKPATH environment variable is not special.

There is no facility for doing file inclusion (gawk's @include mechanism).

There is no facility for dynamically adding new functions written in C (gawk's @load mechanism).

The \x escape sequence. (Disabled with —posix.)

The ability to continue lines after ? and :. (Disabled with —posix.)

Octal and hexadecimal constants in AWK programs.

The ARGIND, BINMODE, ERRNO, LINT, RT and TEXTDOMAIN variables are not special.

The IGNORECASE variable and its side-effects are not available.

The FIELDWIDTHS variable and fixed-width field splitting.

The FPAT variable and field splitting based on field values.

The PROCINFO array is not available.

The use of RS as a regular expression.

The special file names available for I/O redirection are not recognized.

The |& operator for creating co-processes.

The BEGINFILE and ENDFILE special patterns are not available.

The ability to split out individual characters using the null string as the value of FS, and as the third argument to split().

An optional fourth argument to split() to receive the separator texts.

The optional second argument to the close() function.

The optional third argument to the match() function.

The ability to use positional specifiers with printf and sprintf().

The ability to pass an array to length().

The and(), asort(), asorti(), bindtextdomain(), compl(), dcgettext(), dcngettext(), gensub(), lshift(), mktime(), or(), patsplit(), rshift(), strftime(), strtonum(), systime() and xor() functions.

Localizable strings.

The AWK book does not define the return value of the close() function. Gawk's close() returns the value from fclose(3), or pclose(3), when closing an output file or pipe, respectively. It returns the process's exit status when closing an input pipe. The return value is -1 if the named file, pipe or co-process was not opened with a redirection.

When gawk is invoked with the —traditional option, if the fs argument to the -F option is “t”, then FS is set to the tab character. Note that typing gawk -F\t ... simply causes the