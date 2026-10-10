still used among engineers and scientists but years older and much more primitive. In the Unix world no other compiled languages are in mainstream use. Outside the world of Unix, COBOL is widely used for financial and business software.

There used to be many other compiler languages, but most of them have either become extinct or are strictly research tools. If you are a new Unix developer using a compiled language, it is overwhelmingly likely to be C or C++.

# ## Interpreted Languages

An *interpreted* language depends on an interpreter program that reads the source code and translates it on the fly into computations and system calls. The source has to be reinterpreted (and the interpreter present) each time the code is executed.

Interpreted languages tend to be slower than compiled languages, and often have limited access to the underlying operating system and hardware. On the other hand, they tend to be easier to program and more forgiving of coding errors.

Many Unix utilities, including the shell, bc, sed, and awk, are effectively small interpreted languages. BASHcs are usually interpreted. So is Tcl. Historically, the most important interpretive language has been LISP (a major improvement over most of its successors). Today Perl is very widely used and steadily growing more popular.

# ## P-code Languages

Since 1990, *p-code*, a kind of hybrid language that uses both compilation and interpretation, has become increasingly important. P-code languages are like compiled languages in that the source is translated to a compact binary form you actually execute, but which is not machine code. Instead it's *pseudocode* (or *p-code*), which is usually a lot simpler but more powerful than a real machine language. When you run the program, you interpret the p-code.

P-code can run nearly as fast as a compiled binary (p-code interpreters can be made quite simple, small, and speedy). But p-code languages can keep the flexibility and power of a good interpreter.

Important p-code languages include Python and Java.