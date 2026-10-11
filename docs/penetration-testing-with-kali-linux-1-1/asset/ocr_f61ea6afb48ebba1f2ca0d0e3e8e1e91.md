+   EBX (base): Base pointer for memory addresses
+   ECX (counter): Loop, shift, and rotation counter
+   EDX (data): I/O port addressing, multiplication, and division
+   ESI (source index): Pointer addressing of data and source in string copy operations
+   EDI (destination index): Pointer addressing of data and destination in string copy operations

# 10.1.2.2 ESP - The Stack Pointer

As previously mentioned, the stack is used for storage of data, pointers, and arguments. Since the stack is dynamic and changes constantly during program execution, ESP, the stack pointer, keeps “track” of the most recently referenced location on the stack (top of the stack) by storing a pointer to it.

> A pointer is a reference to an address (or location) in memory. When we say a register “stores a pointer” or “points” to an address, this essentially means that the register is storing that target address.

# 10.1.2.3 EBP - The Base Pointer

Since the stack is in constant flux during the execution of a thread, it can become difficult for a function to locate its own stack frame, which stores the required arguments, local variables, and the return address. EBP, the base pointer, solves this by storing a pointer to the top of the stack when a function is called. By accessing EBP, a function can easily reference information from its own stack frame (via offsets) while executing.

# 10.1.2.4 EIP - The Instruction Pointer

EIP, the instruction pointer, is one of the most important registers for our purposes as it always points to the next code instruction to be executed. Since EIP essentially directs the flow of a program, it is an attacker’s primary target when exploiting any memory corruption vulnerability such as a buffer overflow.

# 10.2 Buffer Overflow Walkthrough

In this section, we will analyze a simple vulnerable application that does not perform proper sanitization of user input. We will analyze the application source code and discover that by passing a specifically crafted argument to the application, we will be able to copy our controlled input string to a smaller-sized stack buffer, eventually overflowing its limits. This overflow will corrupt data on the stack, finally leading to a return address overwrite and complete control over the EIP register.

Controlling EIP is the first step in creating a successful buffer overflow. In this module, we will focus on controlling EIP and in further modules, we will explain how to leverage this into arbitrary code execution.