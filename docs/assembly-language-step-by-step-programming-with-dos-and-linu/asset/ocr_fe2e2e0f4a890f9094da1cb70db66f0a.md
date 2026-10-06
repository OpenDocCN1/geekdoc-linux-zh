useful at all will take hours of testing at minimum. A serious and ambitious application could take weeks—or months—to test thoroughly. A program that takes various kinds of input values and produces various kinds of output should be tested with as many combinations of input values as possible, and you should examine every possible output every time.

Even so, finding every last bug is considered by some to be an impossible ideal. Perhaps—but you should strive to come as close as possible, in an efficient fashion as you can manage. I have a lot more to say about bugs and debugging throughout the rest of this book.

# Errors versus Bugs

In the interest of keeping the Babel effect at bay, I think it's important to carefully draw the distinction between errors and bugs. An error is something wrong with your source code that the assembler or the linker kicks out as unacceptable. An error prevents the assembly or link process from going to completion and will prevent a final .EXE file from being produced.

A bug, by contrast, is a problem discovered during execution of a program under DOS. Bugs are not detected by either the assembler or the linker. Bugs can be benign, as a misspelled word in a screen message or a line positioned on the wrong screen row; or a bug can make your DOS session run off into the bushes and not come back.

Both errors and bugs require that you go back to the text editor and change something in your source code file. The difference here is that most errors are reported with a line number telling you where to go in your source code file to fix the problem. Bugs, on the other hand, are left as an exercise for the student. You have to hunt them down, and neither assembler nor the linker will give you much in the line of clues.

# Debuggers and Debugging

The final, and almost certainly the most painful, part of the assembly language development process is debugging. Debugging is simply the systematic process by which bugs are located and corrected. A debugger is a utility program designed specifically to help you locate and identify bugs.