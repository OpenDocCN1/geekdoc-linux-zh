
The variable **NF** is set to the total number of fields in the input record.

References to non-existent fields (i.e., fields after **$NF**) produce the null-string. However, assigning to a non-existent field (e.g., **$NF+2 = 5**) increases the value of **NF**, creates any intervening fields with the null string as their values, and causes the value of **$0** to be recomputed, with the fields being separated by the value of **OFS**. References to negative numbered fields cause a fatal error. Decrementing **NF** causes the values of fields past the new value to be lost, and the value of **$0** to be recomputed, with the fields being separated by the value of **OFS**.

Assigning a value to an existing field causes the whole record to be rebuilt when **$0** is referenced. Similarly, assigning a value to **$0** causes the record to be resplit, creating new values for the fields.

## Built-in Variables

*Gawk*’s built-in variables are:

**ARGC**
> The number of command line arguments (does not include options to *gawk*, or the program source).

**ARGIND**
> The index in **ARGV** of the current file being processed.

**ARGV**
> Array of command line arguments. The array is indexed from 0 to **ARGC** - 1. Dynamically changing the contents of **ARGV** can control the files used for data.

**BINMODE**
> On non-POSIX systems, specifies use of “binary” mode for all file I/O. Numeric values of 1, 2, or 3, specify that input files, output files, or all files, respectively, should use binary I/O. String values of **r**, or **w** specify that input files, or output files, respectively, should use binary I/O. String values of **rw** or **wr** specify that all files should use binary I/O. Any other string value is treated as **rw**, but generates a warning message.

**CONVFMT**
> The conversion format for numbers, %.6g, by default.

**ENVIRON**
> An array containing the values of the current environment. The array is indexed by the environment variables, each element being the value of that variable (e.g., **ENVIRON**[**“HOME”**] might be */home/arnold*). Changing this array does not affect the environment seen by programs which *gawk* spawns via redirection or the **system**() function.

**ERRNO**
> If a system error occurs either doing a redirection for **getline**, during a read for **getline**, or during a **close**(), then **ERRNO** will contain a string describing the error. The value is subject to translation in non-English locales.

**FIELDWIDTHS**
> A whitespace separated list of field widths. When set, gawk parses the input into fields of fixed width, instead of using the value of the FS variable as the field separator. See Fields, above.

**FILENAME**
> The name of the current input file. If no files are specified on the command line, the value of FILENAME is "-". However, FILENAME is undefined inside the BEGIN rule (unless set by getline).

**FNR**
> The input record number in the current input file.

**FPAT**
> A regular expression describing the contents of the fields in a record. When set, gawk parses the input into fields, where the fields match the regular expression, instead of using the value of the FS variable as the field separator. See Fields, above.

**FS**
> The input field separator, a space by default. See Fields, above.

**FUNCTAB**
> An array whose indices and corresponding values are the names of all the user-defined or extension functions in the program. NOTE: You may not use the delete statement with the FUNCTAB array.

**IGNORECASE**
> Controls the case-sensitivity of all regular expression and string operations. If IGNORECASE has a non-zero value, then string comparisons and pattern matching in rules, field splitting with FS and FPAT, record separating with RS, regular expression matching with ~ and !~, and the gensub(), gsub(), index(), match(), patsplit(), split(), and sub() built-in functions all ignore case when doing regular expression operations. NOTE: Array subscripting is not affected. However, the asort() and asorti() functions are affected.

Thus, if IGNORECASE is not equal to zero, /aB/ matches all of the strings ab, aB, Ab, and AB. As with all Awk variables, the initial value of IGNORECASE is zero, so all regular expression and string operations are normally case-sensitive.

**LINT**
> Provides dynamic control of the --lint option from within an Awk program. When true, gawk prints lint warnings. When false, it does not. When assigned the string value fatal, lint warnings become fatal errors, exactly like --lint=fatal. Any other true value just prints warnings.

**NF**
> The number of fields in the current input record.

**NR**
> The total number of input records seen so far.

**OFMT**
> The output format for numbers, %.6g, by default.

**OFS**
> The output field separator, a space by default.

**ORS**
> The output record separator, by default a newline.

**PREC**
> The working precision of arbitrary precision floating-point numbers, 53 by default.

**PROCINFO**
> The elements of this array provide access to information about the running *awk* program. On some systems, there may be elements in the array, **group1** through "**groupn**" for some *n*, which is the number of supplementary groups that the process has. Use the **in** operator to test for these elements. The following elements are guaranteed to be available:

**PROCINFO[“egid”]**
> The value of the *getegid*(2) system call.

**PROCINFO[“srtftime”]**
> The default time format string for **srtftime**().

**PROCINFO[“euid”]**
> The value of the *geteuid*(2) system call.

**PROCINFO[“FS”]**
> **FS** if field splitting with **FS** is in effect, **FPAT** if field splitting with **FPAT** is in effect, or **FIELDWIDTHS** if field splitting with **FIELDWIDTHS** is in effect.

**PROCINFO[“identifiers”]**
> A subarray, indexed by the names of all identifiers used in the text of the *AWK* program. The values indicate what *gawk* knows about the identifiers after it has finished parsing the program; they are *not* updated while the program runs. For each identifier, the value of the element is one of the following:
>
> - **array**: The identifier is an array.
> - **builtin**: The identifier is a built-in function.
> - **extension**: The identifier is an extension function loaded via **@load** or **-l**.
> - **scalar**: The identifier is a scalar.
> - **untyped**: The identifier is untyped (could be used as a scalar or array, *gawk* doesn’t know yet).
> - **user**: The identifier is a user-defined function.

**PROCINFO[“gid”]**
> The value of the *getgid*(2) system call.

**PROCINFO[“pgpid”]**
> The process group ID of the current process.

**PROCINFO[“pid”]**
> The process ID of the current process.

**PROCINFO[“ppid”]**
> The parent process ID of the current process.

**PROCINFO[“uid”]**
> The value of the *getuid*(2) system call.

**PROCINFO[“sorted_in”]**
> If this element exists in **PROCINFO**, then its value controls the order in which array elements are traversed in **for** loops. Supported values are **@ind_str_asc**, **@ind_num_asc**, **@val_type_asc**, **@val_str_asc**, **@val_num_asc**, **@ind_str_desc**, **@ind_num_desc**, @val_type_desc, @val_str_desc, @val_num_desc, and @unsorted. The value can also be the name of any comparison function defined as follows:

```
function cmp_func(i1, v1, i2, v2)
```

where i1 and i2 are the indices, and v1 and v2 are the corresponding values of the two elements being compared. It should return a number less than, equal to, or greater than 0, depending on how the elements of the array are to be ordered.

**PROCINFO["input", "READ_TIMEOUT"]**
> The timeout in milliseconds for reading data from input, where input is a redirection string or a filename. A value of zero or less than zero means no timeout.

**PROCINFO["mpfr_version"]**
> The version of the GNU MPFR library used for arbitrary precision number support in *gawk*. This entry is not present if MPFR support is not compiled into *gawk*.

**PROCINFO["gmp_version"]**
> The version of the GNU MP library used for arbitrary precision number support in *gawk*. This entry is not present if MPFR support is not compiled into *gawk*.

**PROCINFO["prec_max"]**
> The maximum precision supported by the GNU MPFR library for arbitrary precision floating-point numbers. This entry is not present if MPFR support is not compiled into *gawk*.

**PROCINFO["prec_min"]**
> The minimum precision allowed by the GNU MPFR library for arbitrary precision floating-point numbers. This entry is not present if MPFR support is not compiled into *gawk*.

**PROCINFO["api_major"]**
> The major version of the extension API. This entry is not present if loading dynamic extensions is not available.

**PROCINFO["api_minor"]**
> The minor version of the extension API. This entry is not present if loading dynamic extensions is not available.

**PROCINFO["version"]**
> The version of *gawk*.

**ROUNDMODE**
> The rounding mode to use for arbitrary precision arithmetic on numbers, by default N (IEEE-754 roundTiesToEven mode). The accepted values are N or n for roundTiesToEven, U or u for roundTowardPositive, D or d for roundTowardNegative, Z or z for roundTowardZero, and if your version of GNU MPFR library supports it, A or a for roundTiesToAway.

**RS**
> The input record separator, by default a newline.

**RT**
> The record terminator. *Gawk* sets **RT** to the input text that matched the character or regular expression specified by **RS**.

**RSTART**
> The index of the first character matched by **match()**; 0 if no match. (This implies that character indices start at one.)

**RLENGTH**
> The length of the string matched by **match()**; -1 if no match.

**SUBSEP**
> The character used to separate multiple subscripts in array elements, by default \034.

**SYMTAB**
> An array whose indices are the names of all currently defined global variables and arrays in the program. The array may be used for indirect access to read or write the value of a variable:

```
foo = 5  SYMTAB["foo"] = 4  print foo # prints 4
```

The **isarray()** function may be used to test if an element in **SYMTAB** is an array. You may not use the **delete** statement with the **SYMTAB** array.

**TEXTDOMAIN**
> The text domain of the *AWK* program; used to find the localized translations for the program’s strings.

## Arrays
