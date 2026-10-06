# Coding for Linux 505

The Stack
The Argument
Pointer Table
The Arguments

| | | | | | | |
|---|---|---|---|---|---||}{
| EBP+20: (Other Items) | +16 | Null (0): End of Arg | T | A | C | O | S | 0 |
| EBP+16: Ptr to Env. Var. Table | +12 | Arg(3) | F | O | R | O | |
| EBP+12: Ptr to Arg Table | +8 | Arg(2) | T | I | M | E | 0 |
| EBP-8: 4 (Argument Count) | +4 | Arg(1) | / | s | h | o | w | a | r | g | s | 0 |
| E+4: Return Address | | Arg(0): Program Name | |
| EBP+0: | | | Arguments shown for the invocation: |
| EBP-4: EBP | | ./shwargs TIME FOR TACOS |
| EBP-8: ESI | | |
| EBP-12: EDI | ESP | |
| EBP-16: (Unused memory) | |

**Figure 13.3** RET instruction, command-line arguments.

your code is in, it executes it back into the runtime library code’s shutdown sequence. This RET instruction uses the return address just above EBP to take execution to the shutdown sequence. The shutdown sequence has its own return address, which eventually takes it back into Linux. You don't need to access the return address for anything; and certainly don't change it!

Immediately above the return address, at offset 8 from EBP (as EBP+8) is an integer count of the number of arguments. There will be at least one, because the name of the program is the first command-line argument. (After all, you typed the name on the command line, no?)

Immediately above the argument count, at EBP+12, is a pointer to the argument table. Immediately above that, at EBP+16, is a pointer to the table of environment variable pairs. Reading environment variable pairs is done pretty much the same way as reading command-line arguments, so if you understand one, you won't have much trouble with the other.

# Addressing the Stack Relative to EBP

Our crooked trail to the command-line arguments begins at the address stored in EBP. EBP is your anchor point in the stack. It allows you to access the stack using more than just the PUSH and POP instructions. The stack is just memory, after all, and can be addressed through regis