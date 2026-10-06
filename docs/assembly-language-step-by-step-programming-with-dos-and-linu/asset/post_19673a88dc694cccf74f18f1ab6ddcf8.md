
# Saving and Restoring Registers

One of the odder provisions of the C calling conventions that I described earlier is that a program may not arbitrarily change all general-purpose registers. To me this is dumb; if the operating system doesn't want an application to change certain registers, it should save those register values before handing control to the application. However, we must deal with what is, as they say, and the best way to do that is to just save the registers that must be saved before we begin, and restore them again before we pack it up and go home.

The registers that cannot be changed by a Linux application are EBX, ESP, EBP, ESI, and EDI. You'll notice BOILER.ASM saves these registers onto the stack when the program begins, and restores them from the stack before control returns to Linux.

One very important but extremely nonobvious conclusion you must draw from this requirement to save EBX, ESP, EBP, ESI, and EDI is that the other general-purpose registers may be trashed. Yes, trashed—not only by you. When you call procedures written by other people—primarily in the standard C libraries and in utility libraries such as glibc, they may alter the values in EAX, ECX, and EDX. (The stack pointer ESP is a special case and needs special care of a sort not applicable to other registers.) What this means for you is that you cannot assume (for example) a counter value you're tracking in ECX will be left untouched when you call a C library function as printf. If you're using ECX to count passes through a loop that calls a library function—or any function that you didn't write—you must save your value of ECX on the stack before and restore it after the library function returns. The same applies to EAX and EDX. (EAX is often used to return values from library functions, so it's not a good idea to use it to store counters and addresses when you're making library calls.) If you need to keep their values intact across a call to a library function, you must save them on the stack before the library function is called.

On the other hand, the sacred nature of EBX, EBP, ESI, and EDI means that these registers will keep their values when you make C library calls. What is binding on you is binding on the C library as well. Library functions that must use these registers save and restore them without any attention from you.

# Setting Up a Stack Frame

The stack is extremely important in assembly language work, and this is double true in Linux work, because Linux is a C world, and in C (as in most high-level languages including Pascal) the stack has a central role. The reason for this is simple: Compilers are machines that write assembly language code, and they are not human and clever like you. (Although I've met some people who appear less intelligent than some of your better compilers...) This means a compiler has to use what might seem brute force methods to create its code, and most of these depend heavily on the use of the stack.

Compiler code generation is a doctoral thesis and I won't have much to say about it in this book. One compiler mechanism that bears on Linux assembly work is that of the stack frame. Compilers depend on stack frames to create local variables in functions (in Pascal we call them procedures), and while stack frames are less useful in assembly work, you must understand them, because they provide an easy way to access command-line arguments and environment-variables.

A stack frame is a location on the stack marked as belonging to a particular function. It is basically the region between the addresses contained in two registers: base pointer EBP, and stack pointer ESP. This draws better than it explains; see Figure 13.1.

A stack frame is created by pushing the caller's copy of EBP on the stack to save it, and then copying the caller's stack pointer ESP into register EBP. The first two instructions in any assembly program that honors the C calling conventions are these:

```
push ebp
mov esp, ebp own```

After this, you must leave EBP alone, or if you must use it in a serious pinch make sure you can restore it before the change violates any C library assumptions. (I recommend leaving it alone!) EBP is considered the anchor of your new stack frame, which is the main reason it shouldn't be changed. There are things stored on the stack above (that is, at higher addresses) than your stack frame that often need to be referenced in your code, and EBP is the only safe way to reference them. (These things are shown in Figure 13.1, but I return to them later in this chapter.)

Less obvious is the fact that EBP is also the hide-hole in which you stash the caller's stack pointer value, ESP. This is yet another reason not to change EBP once you create your stack frame.

# The Stack

![](img/5af1f694a521bb214c2fd03b770b346f_486_0.png)

Figure 13.1 A stack frame.

Once EBP is safely anchored as one of your stack frame, the stack pointer is free to move up and down the stack as required. The first things you need to put on the stack, however, are the caller’s values for EBP, ESI, EDI, and EDI, as shown in Figure 13.1. The order in which these three are saved isn’t crucial, but the order I show in Figure 13.1 is customary. They will be popped off the stack when the stack frame is destroyed at the end of your program, handing back to the caller (which in our case is the startup/shutdown code from the C library) the shutdown values those registers had when the startup code called your program as the function main.

But once EBX, ESI, and EDI are there, you can push and pop whatever you need for temporary storage. Calling C functions requires a fair amount of pushing and popping, as we see shortly.

# Destroying a Stack Frame

Before your program ends its execution by returning control to the startup/shutdown code (refer back to Figure 12.2 if this relationship isn't clear), its stack frame must be destroyed. This sounds to many like something wrong is happening, but not so: The stack frame must be destroyed, or your program will crash. "Put away" might be a better term than "destroyed"... but let it pass. What we must do is leave the stack and the sacred registers in the state they were in when your program received control from the startup code.

Your stack must be clean before you destroy the stack frame and return control. This means that any temporary values that you have pushed onto the stack during the program's run must be gone. All that is left on the stack should be the caller's values, and the ESP (the stack pointer) better be pointing to the correct address. To destroy the stack frame, you simply move EBP into ESP and pop EBP:

```
mov esp, ebp
pop ebp
```

That's it! The stack frame is gone, and the sacred registers are now in the state they were in when the startup code handled your program. The file BOILER.ASM I showed earlier (it's on the CD-ROM for this book) is a boilerplate assembly language program. It has a comment header, the three sections [.text], [.data], and [.bss], and all the code necessary to create and destroy a stack frame. In between, you place the code for your own programs.

# The Perks of Protected Mode

I've said plenty of times that x86 protected mode is a wonderful thing, but I've never actually come out and said what it gives you. It's a long list, and I can't cover all in detail while you're just starting out; most of it will be under the covers inside the operating system and nothing you can build into your own programs.

In short, from the perspective of beginning assembly programmers, it comes down to more instructions, more versatile registers, a more stable and predictable environment, and no segments! (Can you tell which part I like best?)

# You Know You Have a 386 or Better

An excellent and underappreciated thing about protected mode is simply: that you're running on a 386 or more advanced Intel processor. There's much less to be concerned about in terms of whether you can use certain instructions as when you're running DOS. Nearly every new processor family that Intel has released added some instructions to the x86 instruction set, and the really big gulf is between the 386 and those CPUs that came before it. Thirty-two-bit protected mode is not present in the 8088, 8086, or 286, so whatever limitations are attached to those processors you can just forget.

# No Segments!

I explained the nature of 32-bit flat model in earlier chapters and won't recap too thoroughly here. Segments still exist in 32-bit protected mode, but as each segment can be as large as 4 GB, all the segments are basically in the same memory space, and thus factor out. (This is why we call it “flat.”) The 32-bit offset address can be considered the sole address for an item, and it may be contained in a single 32-bit register.
