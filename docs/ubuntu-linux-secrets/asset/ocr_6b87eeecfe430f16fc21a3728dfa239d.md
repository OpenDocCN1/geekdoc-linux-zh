# Part 5: Programming in Ubuntu

These command-line parameters are explained in Table 27-2.

| Parameter | Description |
|---|---|
| `-a` | Specify which listings to include in the output |
| `-D` | Included for backward compatibility, but ignored |
| `--defsym` | Define symbol and value before assembling source code |
| `-f` | Fast assemble (skips comments and whitespace) |
| `--gstabs` | Include debugging information for each source code line |
| `--gstabs+` | Include special gdb debugging information |
| `-I` | Specify directories to search for include files |
| `-J` | Do not warn about signed overflows |
| `-K` | Included for backward compatibility, but ignored |
| `-L` | Keep local symbols in the symbol table |
| `--listing-lhs-width` | Set the maximum width of the output data column |
| `--listing-lhs-width2` | Set the maximum width of the output data column for continual lines |
| `--listing-rhs-width` | Set the maximum width of input source lines |
| `--listing-cont-lines` | Set maximum number of lines printed in a list for a single line of input |
| `-o` | Specify name of output object file |
| `-R` | Fold the data section into the text section |
| `--statistics` | Display the maximum space and total time used by assembly |
| `-v` | Display the version number of as |
| `-W` | Do not display warning messages |
| `--` | Use standard input for source files |

The assembler creates an *object file*. The object file contains the operation codes (called OP codes) for the program but isn’t yet in a format to run on the system. The object file must first be linked to any required system libraries (discussed next in the “The GNU Linker” section).

Let’s walk through an example of assembling an assembly language program. First, you’ll need to create a test assembly language program:

```
/*cpuid.s Sample program to extract the processor Vendor ID
.section .data
output:
```