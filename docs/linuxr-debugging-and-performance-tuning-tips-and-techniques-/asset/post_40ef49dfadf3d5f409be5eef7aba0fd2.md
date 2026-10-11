
A word about flag or option variable-naming conventions: Much Unix code uses names of the form `xflg` for any given option letter `x` (for example, `nflg` in the V7 `echo`; `xflg` is also common). This may be great for the program's author, who happens to know what the `x` option does without having to check the documentation. But it's unkind to someone else trying to read the code who doesn't know the meaning of all the option letters by heart. It is much better to use names that convey the option's meaning, such as `no_newline` for `echo`'s `-n` option.

## 2.3.2 GNU `getopt()` and Option Ordering

The standard `getopt()` function stops looking for options as soon as it encounters a command-line argument that doesn't start with a `-`. GNU `getopt()` is different: It scans the entire command line looking for options. As it goes along, it *permutes* (rearranges) the elements of `argv`, so that when it's done, all the options have been moved to the front and code that proceeds to examine `argv[optind]` through `argv[argc-1]` works correctly. In all cases, the special argument `--` terminates option scanning.

You can change the default behavior by using a special first character in `optstring`, as follows:

- `optstring[0]` == `+`
  GNU `getopt()` behaves like standard `getopt()`; it returns options in the order in which they are found, stopping at the first non-option argument. This will also be true if `POSIXLY_CORRECT` exists in the environment.

- `optstring[0]` == `-`
  GNU `getopt()` returns *every* command-line argument, whether or not it represents an argument. In this case, for each such argument, the function returns the integer `1` and sets `optarg` to point to the string.

As for standard `getopt()`, if the first character of `optstring` is a `:`, then GNU `getopt()` distinguishes between “invalid option” and “missing option argument” by returning `?` or `:`, respectively. The `:` in `optstring` can be the second character if the first character is `+` or `-`.

Finally, if an option letter in `optstring` is followed by *two* colon characters, then that option is allowed to have an optional option argument. (Say that three times fast!) Such an argument is deemed to be present if it's in the same `argv` element as the option, and absent otherwise. In the case that it's absent, GNU `getopt()` returns the option letter and sets `optarg` to NULL. For example, given:

```c
while ((c = getopt(argc, argv, "ab::")) != -1)
...
```

For `-bYANKEES`, the return value is `'b'`, and `optarg` points to "YANKEES", while for `-b` or `-b YANKEES`, the return value is still `'b'` but `optarg` is set to NULL. In the latter case, "YANKEES" is a separate command-line argument.

## 2.3.3 Long Options

The `getopt_long()` function handles the parsing of long options of the form described earlier. An additional routine, `getopt_long_only()`, works identically, but it is used for programs where *all* options are long and options begin with a single `-`. Otherwise, both work just like the simpler GNU `getopt()` function. (For brevity, whenever we say “`getopt_long()`,” it’s as if we’d said “`getopt_long()` and `getopt_long_only()”.”) Here are the declarations, from the GNU/Linux `getopt(3)` manpage:

```c
#include <getopt.h>  /* GLIBC */

int getopt_long(int argc, char *const argv[],
   const char *optstring,
   const struct option *longopts, int *longindex);

int getopt_long_only(int argc, char *const argv[],
   const char *optstring,
   const struct option *longopts, int *longindex);
```

The first three arguments are the same as for `getopt()`. The next option is a pointer to an array of `struct option`, which we refer to as the *long options table* and which is described shortly. The `longindex` parameter, if not set to NULL, points to a variable which is filled in with the index in `longopts` of the long option that was found. This is useful for error diagnostics, for example.

### 2.3.3.1 Long Options Table

Long options are described with an array of `struct option` structures. The `struct option` is declared in `<getopt.h>`; it looks like this:

```c
struct option {
    const char *name;
    int has_arg;
    int *flag;
    int val;
};
```

The elements in the structure are as follows:

- `const char *name`
  - This is the name of the option, without any leading dashes, for example, “help” or “verbose”.
- `int has_arg`
  - This describes whether the long option has an argument, and if so, what kind of argument. The value must be one of those presented in Table 2.1.
  - The symbolic constants are macros for the numeric values given in the table. While the numeric values work, the symbolic constants are considerably easier to read, and you should use them instead of the corresponding numbers in any code that you write.
- `int *flag`
  - If this pointer is NULL, then `getopt_long()` returns the value in the `val` field of the structure. If it’s not NULL, the variable it points to is filled in with the value in `val` and `getopt_long()` returns 0. If the flag isn’t NULL but the long option is never seen, then the pointed-to variable is not changed.
- `int val`
  - This is the value to return if the long option is seen or to load into *flag* if flag is not NULL. Typically, if flag is not NULL, then val is a true/false value, such as 1 or 0. On the other hand, if flag is NULL, then val is usually a character constant. If the long option corresponds to a short one, the character constant should be the same one that appears in the optstring argument for this option. (All of this will become clearer shortly when we see some examples.)

Each long option has a single entry with the values appropriately filled in. The last element in the array should have zeros for all the values. The array need not be sorted; `getopt_long()` does a linear search. However, sorting it by long name may make it easier for a programmer to read.

### TABLE 2.1

Values for `has_arg`

| Symbolic constant | Numeric value | Meaning |
| :--------------- | :------------ | :------ |
| no_argument       | 0             | The option does not take an argument. |
| required_argument | 1             | The option requires an argument. |
| optional_argument | 2             | The option’s argument is optional. |

The use of `flag` and `val` seems confusing at first encounter. Let’s step back for a moment and examine why it works the way it does. Most of the time, option processing consists of setting different flag variables when different option letters are seen, like so:

```c
while ((c = getopt(argc, argv, "af: hv")) != -1) {
    switch (c) {
    case 'a':
        do_all = 1;
        break;
    case 'f':
        myfile = optarg;
        break;
    case 'h':
        do_help = 1;
        break;
    case 'v':
        do_verbose = 1;
        break;
    ...               Error handling code here
    }
}
```

When `flag` is not NULL, `getopt_long()` sets the variable for you. This reduces the three cases in the previous switch to one case. Here is an example long options table and the code to go with it:

```c
int do_all, do_help, do_verbose;    /* flag variables */
char *myfile;

struct option longopt[] = {
    { "all",  no_argument,    & do_all,      1 },
    { "file", required_argument, NULL,       'f' },
    { "help", no_argument,    & do_help,     1 },
    { "verbose", no_argument,  & do_verbose,  1 },
    { 0, 0, 0, 0 }
};
...
```

```c
while ((c = getopt_long (argc, argv, ":f:", longopts, NULL)) != -1) {
  switch (c) {
  case 'f':
    myfile = optarg;
    break;
  case 0:
    /* getopt_long() set a variable, just keep going */
    break;
  ...
          Error handling code here
  }
}
```

Notice that the value passed for the `optstring` argument no longer contains 'a', 'h', or 'v'. This means that the corresponding short options are not accepted. To allow both long and short options, you would have to restore the corresponding cases from the first example to the switch.

Practically speaking, you should write your programs such that each short option also has a corresponding long option. In this case, it’s easiest to have `flag` be NULL and `val` be the corresponding single letter.

### 2.3.3.2 Long Options, POSIX Style

The POSIX standard reserves the `-W` option for vendor-specific features. Thus, by definition, `-W` isn’t portable across different systems.

If `W` appears in the `optstring` argument followed by a semicolon (note: not a colon), then `getopt_long()` treats `-Wlongopt` the same as `--longopt`. Thus, in the previous example, change the call to be:

```c
while ((c = getopt_long (argc, argv, ":f:W;", longopts, NULL)) != -1)
```

With this change, `-Wall` is the same as `--all` and `-Wfile=myfile` is the same as `--file=myfile`. The use of a semicolon makes it possible for a program to use `-W` as a regular option, if desired. (For example, GCC uses it as a regular option, whereas gawk uses it for POSIX conformance.)

### 2.3.3.3 `getopt_long()` Return Value Summary

As should be clear by now, `getopt_long()` provides a flexible mechanism for option parsing. Table 2.2 summarizes the possible return values and their meaning.
