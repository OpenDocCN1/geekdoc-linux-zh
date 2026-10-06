
The language accepted by the GNU C compiler includes features that are not of the ANSI standard for the language. Using this option forces gcc to reject these language extensions and accept only standard programming language features.

-traditional Causes gcc to accept only C programming language features that existed in the traditional Kernighan and Ritchie C programming. This option allows you to compile correctly older programs using the traditional C language that existed before the ANSI standard C language was defined.

-Dname=value Usually #define preprocessor directives are given in header, or include, files. You can use this option to define symbolic names on the command line. For example, -DLux is equivalent to having the line #define Linux in an include file, and -DMACH=i586 is the same as #define MACH i586.

-fpic Causes gcc to produce position-independent code, which is suitable for installing a shared library.

-twirl-strings By default, the GNU C compiler places strings into protected memory, where they cannot be changed. Some (usually older) programs assume that you can modify string constants. This option changes the behavior of gcc so string constants can be modified.

## Notes

The preceding list of options is only a small fraction of the full set of options available with the GNU C compiler. See the gcc option info page for a complete list.
Although the -o option is generally used to specify a filename to store object code, this option can also be used to use name files resulting from other compilation steps. In the following example the -o option causes the assembly language produced by the following gcc command to be stored in the file acode instead of pgm.s.

```
$ gcc -S -o code pgm.c
```

The lint utility found in many UNIX systems is not available on GNU/Linux. However, the -Wall option performs many of the same checks and can be used in place of lint (page 859).

The conventions used by the C compiler for assigning filename extensions are summarized in Table III-18.

## Examples

The first example compiles, assembles, and links a single C program, compute.c. The executable output is put in a.out. The gcc utility deletes the object file:

```
$ gcc compute.c
```

### Filename Extension // Table III-18

| | |
|---|---|
| .a | Library of object modules |
| .c | C language source file |
| .C, .cc, or .cxx | C++ language source file |
| .i | Preprocessed C language source file |
| .ii | Preprocessed C++ language source file |
| .o | Object file |
| .s | Assembly language source file |
| .S | Assembly language source file that needs preprocessing |

The next example compiles the same program, using the C optimizer (-O option). It assembles and links the optimized code. The -o option causes gcc to put the executable output in `compute`:

```
$ gcc -o compute compute.c
```

Next, a source file, an assembly language file, and an object file are compiled, assembled, and linked. The executable output goes to progo:

```
$ gcc -o progo proc.c profast.s proout.o
```

In the next example gcc searches the standard math library stored in /lib/libm.a when it is linking the himath program and places the executable output in a.out:

```
$ gcc himath.c -lm
```

In the next example, the C compiler compiles topo.c with options that check the code for questionable source practices (the-Wall option) and violations of the ANSI C standard (-pedantic option). The -g option embeds debugging support in the executable file, which is saved in topo with the -o option. Full optimization is enabled with the -O3 option.

The warnings produced by the C compiler are displayed on standard output. In this example the first and last warnings result from the -pedantic option; the other warnings result from the -Wall option:

```
$ gcc -Wall -g -O3 -pedantic -o topo topo.c
In file included from topo.c:2:
/usr/include/ctype.h:65: warning: comma at end of enumerator list
topo.c:13: warning: return-type defaults to 'int'
topo.c:14: In function 'main':
topo.c:14: warning: unused variable 'c'
topo.c:2: In function 'getline':
topo.c:44: warning: 'c' might be used uninitialized in this function
```

When compiling programs that use the X11 include files and libraries, you may need to use the -I and -L options to tell gcc where to locate those include files and libraries. The next example uses those options and also instructs gcc to link the program with the basic X11 library:

```
$ gcc -I/usr/X11R/include plot.c -L/usr/X11R/lib -X11
```

## grep

Searches for a pattern in files
grep [options] pattern [file-list]
The grep utility searches for one or more files, line by line, for a pattern, which can be a simple string or another form of a regular expression. The grep utility takes various actions, specified by options, each time it finds a line that contains a match for the pattern. The grep utility takes its input from files you specify on the command line or from standard input.

## Arguments

The pattern is a regular expression, as defined in Appendix A. You must quote regular expressions that contain special characters, SPACEs, or TABs. An easy way to quote these characters is to enclose the entire expression within single quotation marks. The file-list contains pathnames of ordinary files that grep searches.

## Options

Without any options grep sends lines that contain a match for pattern to standard output. When you specify more than one file on the command line, grep precedes each line that it displays with the name of the file that it came from and a colon.

## Major Options

You can use only one of the following three options at a time. Normally you do not need to use any, as grep defaults to -G, which is regular grep.

- -G grep Interprets pattern as a basic regular expression. This is the default major option if none is specified.
- -E extended Interprets pattern as an extended regular expression (page 1392). The command grep -E is the same as egrep. See "Notes," following.
- -F fixed Interprets pattern as a fixed string of characters. The command grep -F is the same as grep.

## Other Options

- --count -c Displays only the number of lines that contain a match in each file.
- --filename -h If more than one file is given on the command line, does not precede each line of output with the name of the file containing it.

```
--ignore-case -i Causes lowercase letters in the pattern to match uppercase letters in the file and
v versa. Use this option when searching for a word that may be at the beginning
of a sentence (that is, may or may not start with an uppercase letter).
```

```
--files-with-matches -l Displays only the name of each file that contains one or more matches. It dis-plays each filename only once, even if the file contains more than one match.
```

```
--line-number -n Precedes each line by its line number in the file. The file does not need to con-tain line numbers. This number represents the number of lines in the file up to and
the displayed line.
```

```
--quiet -q Does not send anything to stdout; only sets the exit code.
```

```
--recursive -r Recursively descends and processes directories in file-list.
```

```
--no-messages -s Does not display an error message if a file in file-list does not exist or is not readable.
```

```
--invert-match -v Causes lines not containing a match to satisfy the search. When you use
 option by itself, grep displays all lines that do not contain a match for the pattern.
```

```
--word-regexp -w With this option, the pattern must match a whole word. This is helpful if
you are searching for a specific word that may appear as a substring of another
word in the file.
```

## Notes

The grep utility returns an exit status of 0 if it finds a match, 1 if it does not find a, and 2 if the file is not accessible or there is a syntax error.

Two utilities perform functions similar to that of grep. The egrep utility (same
as grep -E) allows you to use extended regular expressions (page 1392), which in-cludes a different set of special characters than basic regular expressions do
(page 1390). GNU grep, which is the grep that is included with Red Hat Linux, uses
regular expressions in place of regular expressions. Thus egrep is virtually the same
as grep. Refer to the grep info page for a minimal distinction.

## Examples

The following examples assume that the working directory contains three files:
testa, testb, and testc. The contents of each file are

| File testa | File testb | File testc |
|---|---|---|
| aaabb | aaaaa | AAAAA |
| bbbbb | bbbbb | BBBBB |
| ff-ff |ccccc | CCCCC |
| ccccd | ddddd | DDDDD |
| dddaa | | |
