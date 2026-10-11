
software. The "no arbitrary limits" principle is perhaps the single most important of these. This document is required reading for serious programmers.

Making programs portable is a significant challenge. Guidelines and tools help, but ultimately experience is needed too.

## Exercises

1. Read and comment on the article “The GNU Project”[11] by Richard M. Stallman, originally written in August of 1998.
   [11] http://www.gnu.org/gnu/thegnuproject.html

# Chapter 2

![](img/766b5597246d532412fad21b1c59ccec_55_0.png)

# Arguments, Options, and the Environment

In this chapter:

- 2.1 Option and Argument Conventions page 24
- 2.2 Basic Command-Line Processing page 28
- 2.3 Option Parsing: getopt() and getopt_long() page 30
- 2.4 The Environment page 40
- 2.5 Summary page 49
- Exercises page 50

Command-line option and argument interpretation is usually the first task of any program. This chapter examines how C (and C++) programs access their command-line arguments, describes standard routines for parsing options, and takes a look at the environment.

## 2.1 Option and Argument Conventions

The word *arguments* has two meanings. The more technical definition is “all the ‘words’ on the command line.” For example:

```
$ ls main.c opts.c process.c
```

Here, the user typed four ‘words’. All four words are made available to the program as its arguments.

The second definition is more informal: Arguments are all the words on the command line *except* the command name. By default, Unix shells separate arguments from each other with *whitespace* (spaces or TAB characters). Quoting allows arguments to include whitespace:

```
$ echo here are lots    of spaces
     here are lots  of spaces
     																		The shell “eats” the spaces
$ echo "here are lots     of spaces"
     here are lots    of spaces
     																		Spaces are preserved
```

Quoting is transparent to the running program; `echo` never sees the double-quote characters. (Double and single quotes are different in the shell; a discussion of the rules is beyond the scope of this book, which focuses on C programming.)

Arguments can be further classified as *options* or *operands*. In the previous two examples all the arguments were operands: files for `ls` and raw text for `echo`.

Options are special arguments that each program interprets. Options change a program’s behavior, or they provide information to the program. By ancient convention, (almost) universally adhered to, options start with a dash (a.k.a. hyphen, minus sign) and consist of a single letter. *Option arguments* are information needed by an option, as opposed to regular operand arguments. For example, the `fgrep` program’s `-f` option means “use the contents of the following file as a list of strings to search for.” See Figure 2.1.

# 2.1 Option and Argument Conventions

![](img/766b5597246d532412fad21b1c59ccec_57_0.png)

Thus, `patfile` is not a data file to search, but rather it's for use by `fgrep` in defining the list of strings to search for.

### 2.1.1 POSIX Conventions

The POSIX standard describes a number of conventions that standard-conforming programs adhere to. Nothing requires that your programs adhere to these standards, but it's a good idea for them to do so: Linux and Unix users the world over understand and use these conventions, and if your program doesn't follow them, your users will be unhappy. (Or you won't have any users!) Furthermore, the functions we discuss later in this chapter relieve you of the burden of manually adhering to these conventions for each program you write. Here they are, paraphrased from the standard:

1. Program names should have no less than two and no more than nine characters.
2. Program names should consist of only lowercase letters and digits.
3. Option names should be single alphanumeric characters. Multidigit options should not be allowed. For vendors implementing the POSIX utilities, the `-W` option is reserved for vendor-specific options.
4. All options should begin with a `-` character.
5. For options that don't require option arguments, it should be possible to group multiple options after a single `-` character. (For example, `foo -a -b -c` and `foo -abc` should be treated the same way.)
6. When an option does require an option argument, the argument should be separated from the option by a space (for example, `fgrep -f patfile`).

The standard, however, does allow for historical practice, whereby sometimes the option and the operand could be in the same string: `fgrep -fpatfile`. In practice, the `getopt()` and `getopt_long()` functions interpret `-fpatfile` as `-f patfile`, not as `-f -p -a -t . . . .`.

7. Option arguments should not be optional.
   This means that when a program documents an option as requiring an option argument, that option’s argument must always be present or else the program will fail. GNU `getopt()` does provide for optional option arguments since they’re occasionally useful.
8. If an option takes an argument that may have multiple values, the program should receive that argument as a single string, with values separated by commas or whitespace.
   For example, suppose a hypothetical program `myprog` requires a list of users for its `-u` option. Then, it should be invoked in one of these two ways:
   - `myprog -u "arnold,joe,jane"` (Separate with commas)
   - `myprog -u "arnold joe jane"` (Separate with whitespace)
   In such a case, you’re on your own for splitting out and processing each value (that is, there is no standard routine), but doing so manually is usually straightforward.
9. Options should come first on the command line, before operands. Unix versions of `getopt()` enforce this convention. GNU `getopt()` does not by default, although you can tell it to.
10. The special argument `--` indicates the end of all options. Any subsequent arguments on the command line are treated as operands, even if they begin with a dash.
11. The order in which options are given should not matter. However, for mutually exclusive options, when one option overrides the setting of another, then (so to speak) the last one wins. If an option that has arguments is repeated, the program should process the arguments in order. For example, `myprog -u arnold -u jane` is the same as `myprog -u "arnold,jane"`. (You have to enforce this yourself; `getopt()` doesn’t help you.)
12. It is OK for the order of operands to matter to a program. Each program should document such things.
13. Programs that read or write named files should treat the single argument `-` as meaning standard input or standard output, as is appropriate for the program.

Note that many standard programs don't follow all of the above conventions. The primary reason is historical compatibility; many such programs predate the codifying of these conventions.

### 2.1.2 GNU Long Options

As we saw in Section 1.4.2, “Program Behavior,” page 16, GNU programs are encouraged to use long options of the form `--help`, `--verbose`, and so on. Such options, since they start with `--`, do not conflict with the POSIX conventions. They also can be easier to remember, and they provide the opportunity for consistency across all GNU utilities. (For example, `-help` is the same everywhere, as compared with `-h` for “help,” `-i` for “information,” and so on.) GNU long options have their own conventions, implemented by the `getopt_long()` function:

1. For programs implementing POSIX utilities, every short (single-letter) option should also have a long option.
2. Additional GNU-specific long options need not have a corresponding short option, but we recommend that they do.
3. Long options can be abbreviated to the shortest string that remains unique. For example, if there are two options `--verbose` and `--verbatim`, the shortest possible abbreviations are `--verbo` and `--verva`.
4. Option arguments are separated from long options either by whitespace or by an `=` sign. For example, `--sourcefile=/some/file` or `--sourcefile /some/file`.
5. Options and arguments may be interspersed with operands on the command line; `getopt_long()` will rearrange things so that all options are processed and then all operands are available sequentially. (This behavior can be suppressed.)
6. Option arguments can be optional. For such options, the argument is deemed to be present if it's in the same string as the option. This works only for short options. For example, if `-x` is such an option, given `foo -xYANK'EE'S -y`, the argument to `-x` is `YANK'EE'S`. For `foo -x -y`, there is no argument to `-x`.
