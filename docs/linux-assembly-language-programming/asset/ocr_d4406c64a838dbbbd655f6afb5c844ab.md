224 unsigned or -32 signed, then everything would be okay. Two hundred twenty-four is the two's complement positive that is equivalent to -32 in the eight-bit system. But we're not content with eight bits. We want 16. And

$-32 \equiv 480 \pmod{65,536}$ is wrong.

In the 16-bit system, -32 is represented by 65504, not 480. Consequently, we can't use MUL (or DIV) for both signed and unsigned numbers. MUL and DIV work for unsigned numbers. There are different commands which work for signed numbers: IMUL and IDIV. This is an example of the issue raised in section 3.6.5.

# **Further Reading**

+   * The Microprocessor, A Biography, Michael S.Malone, Springer: 1995.
+   * The Anatomy of a High-Performance Microprocessor, Shriver and Smith, IEEE: 1998.

# # Chapter 4. ASSEMBLY LANGUAGE

A computer program is something which can be stored in a computer's memory. If the memory has one-byte words, we can then say that the computer program consists of bytes. These bytes are also called *machine language*. Writing a program by listing these bytes explicitly is called *machine language programming*. It is the original form of programming. It is definitely the most tedious. Assembly language was devised as a way of specifying machine code without actually having to write it down. Assembly language may be mere shorthand or it may involve complex *macros*, some of which may even resemble *if* or *while* statements in C. But whether it is primitive or fancy, its defining characteristic is that it gives the programmer control over the machine language.

Three good reasons for learning assembly language are

+   1. In truly time-critical sections of code, it is sometimes possible to improve performance by coding in assembly language.
+   2. It is a good way to learn how a particular CPU works.
+   3. In writing a new operating system or in porting an existing system to a new machine, there are sections of code which must be written in assembly language.

Assembly languages are written to fit hand-in-glove with a specific processor. Given the considerable variety of processors and instruction sets, one might expect there to be a considerable variety in the instruction formats for the various assembly languages as well. But this is not the case. Assembly languages generally follow one universal format which might be called the *four field format*.

# ## 4.1 The Four Field Format

According to this format every assembly language program consists of lines. Every line consists of four fields. The four fields are the label field, the mnemonic field, the operand field, and the comment field.

+   1. The label field is used for a label which specifies the target of a jump instruction. A jump is the same as a *go to* instruction. Examples of jump instructions are given in section 4.4.
+   2. The mnemonic field contains an instruction specifier. Examples of mnemonics are MOV, ADD, SUB, etc. The word *mnemonic* suggests that it makes the machine code easy to remember, although it doesn't; it makes the machine code unnecessary to remember.
+   3. The operand field contains the object or objects on which the instruction is operating. If there is more than one operand, they are separated by commas. As we noticed above, ADD takes two operands. JMP