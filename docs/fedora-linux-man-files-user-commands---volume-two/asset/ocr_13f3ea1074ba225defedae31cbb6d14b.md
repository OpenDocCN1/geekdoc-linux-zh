@val_type_desc, @val_str_desc, @val_num_desc, and @unsorted. The value can also be the name of any comparison function defined as follows:

```
function cmp_func(i1, v1, i2, v2)
```

where i1 and i2 are the indices, and v1 and v2 are the corresponding values of the two elements being compared. It should return a number less than, equal to, or greater than 0, depending on how the elements of the array are to be ordered.

**PROCINFO["input", "READ_TIMEOUT"]** The timeout in milliseconds for reading data from input, where input is a redirection string or a filename. A value of zero or less than zero means no timeout. **PROCINFO["mpfr_version"]** The version of the GNU MPFR library used for arbitrary precision number support in *gawk*. This entry is not present if MPFR support is not compiled into *gawk*. **PROCINFO["gmp_version"]** The version of the GNU MP library used for arbitrary precision number support in *gawk*. This entry is not present if MPFR support is not compiled into *gawk*.

**PROCINFO["prec_max"]** The maximum precision supported by the GNU MPFR library for arbitrary precision floating-point numbers. This entry is not present if MPFR support is not compiled into *gawk*. **PROCINFO["prec_min"]** The minimum precision allowed by the GNU MPFR library for arbitrary precision floating-point numbers. This entry is not present if MPFR support is not compiled into *gawk*.

**PROCINFO["api_major"]** The major version of the extension API. This entry is not present if loading dynamic extensions is not available. **PROCINFO["api_minor"]** The minor version of the extension API. This entry is not present if loading dynamic extensions is not available. **PROCINFO["version"]** The version of *gawk*.

**ROUNDMODE** The rounding mode to use for arbitrary precision arithmetic on numbers, by default N (IEEE-754 roundTiesToEven mode). The accepted values are N or n for roundTiesToEven, U or u for roundTowardPositive, D or d for roundTowardNegative, Z or z for roundTowardZero, and if your version of GNU MPFR library supports it, A or a for roundTiesToAway. **RS** The input record separator, by default a newline. **RT** The record terminator. *Gawk* sets **RT** to the input text that matched the character or regular expression specified by **RS**. **RSTART** The index of the first character matched by **match()**; 0 if no match. (This implies that character indices start at one.) **RLENGTH** The length of the string matched by **match()**; -1 if no match. **SUBSEP** The character used to separate multiple subscripts in array elements, by default \034. **SYMTAB** An array whose indices are the names of all currently defined global variables and arrays in the program. The array may be used for indirect access to read or write the value of a variable:

```
foo = 5  SYMTAB["foo"] = 4  print foo # prints 4
```

The **isarray()** function may be used to test if an element in **SYMTAB** is an array. You may not use the **delete** statement with the **SYMTAB** array.

**TEXTDOMAIN** The text domain of the *AWK* program; used to find the localized translations for the program’s strings.

# ### Arrays