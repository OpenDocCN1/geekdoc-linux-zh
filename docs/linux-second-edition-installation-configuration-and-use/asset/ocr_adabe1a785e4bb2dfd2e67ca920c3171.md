# ALPHABETICAL COMMAND REFERENCE 453

programming, and is used to output information for the user during execution of a shell script. When the character string contains spaces or special characters, it must be enclosed in single or double quotes (see also page 399).

# expand [options] file

expand substitutes all tab characters with a corresponding number of spaces. When no options are specified, expand assumes a tabulator distance of eight characters. The result is displayed on screen and can be redirected into a file by means of >.

-n changes the tabulator distance to n characters.

# expr expression

expr evaluates the specified expression arithmetically or performs a pattern match for character strings. The specified variables, numbers and operators must be separated by spaces. A short description of all permitted operators can be found in the man for expr.

When you use the bash as a shell, you can also calculate without using expr by simply entering arithmetic expressions in the form $[expression].

# Example

```
user expr 2 + 3
yields the result 5.
```

# fdformat [-n] drive

fdformat carries out low-level formatting of a diskette. A disk prepared in this way can subsequently be used to install a file system with mformat or mkfs. To write a backup copy with tar or to write a boot kernel with dd (see pages 468-468, 450-483).

The option -n prevents a subsequent verification of the diskette. The disk is specified by means of a device file, for example /dev/fd0H140 for formatting a 3.5-inch HD disk in drive A. The following device files are commonly used:

| /dev/fd0 | 3.5-inch HD in A: (default 1.4 MBytes) |
| /dev/fd0d360 | 5.25-inch diskette in A: |
| /dev/fd0720 | 3.5-inch diskette DD in A: |
| /dev/fd0H140 | 3.5-inch HD in A: |
| /dev/fd02880 | 3.5-inch diskette with 2.88 MBytes in A: |
| /dev/fd1360 | 5.25-inch diskette in B: |
| /dev/fd10720 | 3.5-inch diskette DD in B: |
| /dev/fd11200 | 3.5-inch HD in B: |

If you use fdformat without having previously accessed the diskette, command comes with the error message 'no such device.' This can be remedied with