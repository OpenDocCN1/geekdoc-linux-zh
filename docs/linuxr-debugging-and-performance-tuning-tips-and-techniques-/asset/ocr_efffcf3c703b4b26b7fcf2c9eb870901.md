```
<?func?
$ factorial -#d 1 2    *Show debugging messages from `DBUG_PRINT()`*
?f?unc?: args: argv[2] = 1
factorial: find: find 1 factorial
factorial: result: result is 1
1
?f?unc?: args: argv[3] = 2
factorial: find: find 2 factorial
factorial: find: find 1 factorial
factorial: result: result is 1
factorial: result: result is 2
2
```

The -# option controls the `debug` library. It is “special” in the sense that `DBUG_PUSH()` will accept the entire string, ignoring the leading “-#” characters, although you could use a different option if you wish, passing `DBUG_PUSH()` just the option argument string (this is optional if you use `getopt()`).

The control string consists of a set of options and arguments. Each group of options and arguments is separated from the others by a colon character. Each option is a single letter, and the arguments to that option are separated from it by commas. For example:

```
$ myprog -#d,m;1:;f,check_salary,check_start_date -f infile -o outfile
```

The *d* option enables `DBUG_PRINT()` output, but only if the first argument string is one of "mem" or "ipc". (With no arguments, all `DBUG_PRINT()` messages are printed.) Similarly, the *f* option limits the function call trace to just the named functions: `check_salary()`, and `check_start_date()`.

The following list of options and arguments is reproduced from the `debug` library manual. Square brackets enclose optional arguments. We include here only the ones we find useful; see the documentation for the full list.

+   - *d*[*,*keywords*]
+     - Enable output from macros with specified *keywords*. A null list of keywords implies that all keywords are selected.
+   - *F*
+     - Mark each debugger output line with the name of the source file containing the macro causing the output.