# 12.5 x86 unleashed 237

Table 12.3 GCC Inline Assembly Constraints

| Constraint | Variable Referenced As |
|---|---|
| r | Any general purpose register |
| m | Memory operand |
| o | Offset operand (e.g., -4(%esp)) |
| i | Immediate integer operand |
| E | Immediate floating point operand |
| a | RAX or EAX |
| b | RBX or EBX |
| c | RCX or ECX |
| d | RDX or EDX |
| S | RSI or ESI |
| D | RDI or EDI |
| x | Any SSE register |

The optional `volatile` attribute informs the compiler that the instructions have side-effects not visible to the compiler. This prevents the compiler from optimizing these instructions out of the executable and from significantly moving the instructions.
The input and output variables are a comma delimited list of variables of the form `[name]constraint`. A list of popular constraints on x86 is found in Table 12.3. Constraints can be modified with prefixes. Input operands must be marked as volatile, with either `=` which specifies that the operand is write-only, or `+` which specifies that the operand is read and written. Be careful with constraints, as incorrect constraints can lead to miscompiled programs.
The clobbered list is a comma delimited list of strings, each containing the names of the registers they modify. There are also two resources that can be specified in the clobbered list, `memory`, which informs the compiler that memory was changed, and `cc`, which informs the compiler that the EFLAGS condition was changed. Resources clobbered in the input and output lists do not need to be listed in the clobbered list.
When writing inline, the author recommends testing the constraints on multiple compilers, as some compilers, such as LLVM, are significantly more restrictive in what they accept. At the time of this writing, ICC will complain if there are empty lists at the end of the declaration.

# 12.5.3 COMPILER INTRINSICS

Compiler intrinsics are built-in functions provided by the compiler that share a one-to-one, or many-to-one, relationship with specific instructions. This allows the specific instructions to be written using high-level programming constructs and frees the developer from worrying about calling conventions, register allocation, and