# Exploring GCC options

Here is the basic syntax of the `gcc` command:

```
```
 gcc options filenames
```
```

Each option starts with a hyphen (`-`) and usually has a long name, such as `-funsigned-char` or `-finline-functions`. Many commonly used options are short, however, such as `-c`, to compile only, and `-g`, to generate debugging information (needed to debug the program by using the GNU debugger, gdb).

You can view a summary of all GCC options by typing the following command in a terminal window:

```
```bash
man gcc
```
```

Then you can browse through the commonly used GCC options. Usually, you don't have to provide GCC options explicitly because the default settings are fine for most applications. Table 1-1 lists some of the GCC options you may use.

Table 1-1 Commonly Used GCC Options
| Option | Meaning |
| --- | --- |
| -ansi | Support ANSI standard C (ISO C89) syntax only. (This option disables some GNU C-specific features, such as the asm and typeof keywords.) |
| -c | Compile and generate object file only. |
| -DMACRO | Define the macro with the string "1" as its value. |
| -DMACRO=DEFN | Define the macro as DEFN where DEFN is some text string. |
| -E | Run only the C preprocessor. |
| -fallow-single-precision | Perform all math operations in single precision. |
| -fpcc-struct-return | Return all struct and union values in memory, rather than return in registers. (Returning values this way is less efficient, but at least it's compatible with other compilers.) |
| -fPIC | Generate position-independent code (PIC) suitable for use in a shared library. |
| -freg-struct-return | When possible, return struct and union values in registers. |
| -g | Generate debugging information. (The GNU debugger can use this information.) |

(continued)