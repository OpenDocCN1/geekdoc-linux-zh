# regcmp

Instead of numbering references, use labels from the senior author's last name and the year of publication. Use only the first m digits of the last name and the last n digits of the date. If you omit more n, use the entire name or date.

+   -lm, n

+   -n
Do search the default file.

+   -p filename
Take the next argument as a file of references to be searched. Search the default file list.
Sort references by fields whose key letters are in the keys string and permute reference numbers in the text accordingly. Using this option also uses the -e option. You can follow the key letters with a number indicating how many fields are used. Use a + sign to indicate a very large number. The default is AD, which sorts on the senior author and date. For example, to sort on all authors and the date, use the option SA+T.

# Files

+   /usr/lib/refer
Directory of programs.

+   /usr/lib/refer/papers
Directory of default publication lists and indexes.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNdoc |

# See Also

addbib(1), eqn(1), indbib(1), lookbib(1), nroff(1), roffbib(1), sortbib(1), tbl(1), troff(1), attributes(5)

# regcmp — Compile Regular Expressions

# Synopsis

```
/usr/ccs/bin/regcmp [-] filename...
```

# Description

The regcmp command performs a function similar to the regcmp(3C) language library function. In most cases, the regcmp(1) command precludes the need for calling the regcmp(3C) from C programs. Bypassing regcmp(3C) saves on execution time and program size. The regcmp command compiles the regular expressions in filename and puts the output in filename.