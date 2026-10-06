# The Programmer's View of Linux

"a.out," every time—irrespective of what your object file or source files are called.

# Why Not gas?

You might be wondering why, if there's a perfectly good assembler installed automatically with every copy of Linux, I'm bothering to show you how to install and use another one. First of all, there is no gas like DOS as best I know, so you can't take your first steps in gas assembly while working with DOS. But more important, gas uses a peculiar syntax that is utterly unlike that of all the other familiar assemblers used in the x86 (MASM and TASM as NASM) and a whole set of instruction mnemonics unique to itself. I find them unintuitive and hard to read. This is the AT&T syntax, because it was created by AT&T as a portable assembly notation to make Unix easier to port from one underlying CPU to another. It's ugly because it was designed to be generic, and it can be recast for any reasonable CPU you come up with. (Don't forget that Unix predicates the x86, and gas's predecessor is older than the x86).

If it were simple, I wouldn't mention gas at all, since you don't need to use it to write Linux code in NASM. However, one of the major ways you'll end up learning many of the standard C library calls is by using them in short C programs and then inspecting the assembly output gcc generates (I have more to say about this later on.) What gcc generates when it compiles a C program is a file (with a .extension) of assembly source code using the AT&T syntax and mnemonics. It may not be necessary to learn the AT&T syntax thoroughly enough to write it, but it will be very helpful if you can pick it well enough to read it. I'll show you an example later on, and when I do I will summarize the important differences between AT&T and the NASM syntax and mnemonics, which are more properly coded the Intel syntax and mnemonics.

# The make Utility and Dependencies

If you've done any programming in C at all, you're almost certainly familiar with the idea of the make utility. The make mechanism grew up in the C world, and although it's been adopted by many other programming languages and environments, it's never been adopted as thoroughly (or as nakedly) as in the C world.