Of these, the CONTROL key deserves special mention. A large number of UNIX commands are executed by holding down the CONTROL key while simultaneously pressing another key. For example, on many terminals the erase function can be invoked by the key combination

CONTROL-H

When referring to this combination of keys in print, you will often see the notation ^H, where the caret (^) stands for the CONTROL key.

Later in the book, you will learn about many of the functions that involve the CONTROL key. For now, there are four special functions that you should ask about:

| Function | Purpose | Key Combination | Alternative |
| :------- | :------ | :--------------- | :---------- |
| erase    | deletes a character | CONTROL-H | ^H, BACKSPACE |
| interrupt | stops a program | CONTROL-C | ^C, DELETE |
| stop    | freezes the terminal | CONTROL-S | ^S, ? |
| continue | unfreezes the terminal | CONTROL-Q | ^Q, ? |

Note that there may be more than one way to delete a character or interrupt a program. As shown in Appendix A, UNIX provides a way for you to change the keys that invoke these functions.

# 2.9 Printer Codes

Almost every UNIX system has a printer for producing paper output. (Paper output is called hardcopy.) A large computer installation may have many printers. Individual printers are identified by a code name, which typically reflects the type and location of the device. For example, suppose that one of the printers connected to your UNIX system were an Apple LaserWriter 360, located in Room 12. The system administrator might give this printer one of the following code names:

alw360-12

1w360r12

room121w

You get the idea. There are no standard rules on naming printers, so it is a good idea to ask your system administrator for the names of the printers that are part of your system.

Your system
administrator can tell
you which keys
perform these
functions.