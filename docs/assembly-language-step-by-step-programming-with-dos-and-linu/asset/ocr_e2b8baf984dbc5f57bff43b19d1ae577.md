in this chapter. Finally, procedure libraries themselves may share data and procedures in any combination, as long as the declarations are handled correctly.

We sometimes say that a program or module containing procedures or variables declared as public exports those items. Also, we say that a program or module that uses procedures or variables that are external to it imports those items.

# The Mechanics of Globals and Externals

I've described the source code mechanics of assembly language programs in detail in the last few chapters. External modules are similar to programs. There are two major differences, concerning things that external modules lack:

+   - External modules do not contain a main program and have no start address. That is, no label .start: exists to indicate to the linker that this is the point at code execution is to begin. External modules are not intended to be run by themselves, so a start address is both unnecessary and (if one one were added) a temptation to chaos.

+   - External modules have no stack segment. This is not an absolute requirement (there are few such requirements in assembler work), but for simple assembly language programming it's true enough. Your stack segment should be defined in your main program module. External modules should have none—the one defined by the programs that call them. Recall that in real mode segmented model, there is only one stack in operation at any given time, and the one you define in your program is used by everything running on your machine—including the operating system—while your program has control.

External modules may have a data segment. If the external is to define a variable that is to be shared by the main program or by other externals, it obviously must have a data segment for that variable to reside in. But less obviously, if the external is to share a variable with another external or with the main program, it must still define a data segment, even if that data segment is empty except for the external declaration.

If a segment (whether a code segment or a data segment) is to export anything, that segment must be declared public. This is done with the