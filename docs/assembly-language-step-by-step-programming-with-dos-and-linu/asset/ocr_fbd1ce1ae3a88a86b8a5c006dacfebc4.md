ing value in EAX becomes the offset, when added to the address represented by nl, gives you the address of the place in the string where printf should begin outputting.

Having the data right in the subroutine means that it's easy to cut and paste the subroutine from one program into another without leaving the essential table of newline characters behind. And because the only code that ever uses the newline line is the subroutine itself, there's no benefit to placing the newline table in the more centrally visible [data] section.

# Accessing Command-Line Arguments

One of the most useful things is to be able to do when writing simple utilities is to pass them parameters—C people call them arguments—on the command line. If you're working in C or Pascal, these are set up as predefined arrays or functions and are a snap to use. In assembly, there's no such convenience (Surprise!) You have to know where and how they're stored, which is (alas) nontrivial.

On the other hand, getting at command-line arguments is a wonderful exercise both in the use of pointers and also of accessing the stack memory from EBP, where a number of interesting things live. EBP is your marker driven into the stack, and it anchors your access to both your own items (stored down-memory from EBP) and those owned by the runtime library, which are up-memory.

Because we're talking about a pointer to a table of pointers to the actual argument strings, the best way to begin is to draw a picture of the lay of the land. Figure 13.3 shows the pointer relationships and stack structures we have to understand to identify and read the command-line arguments.

As I explained earlier in this chapter, Linux passes control to your program, the C library's startup code gets control first, and it sets up a number of things for you, before the code that you write begins executing. One of the things the startup code does is set up your program's access to the command-line arguments. It does this by building a table of pointers to the arguments and placing a pointer to that table on the stack, up-memory from EBP.

The startup code places other things on the stack as well. Immediately above EBP is the return address for your portion of the code. When