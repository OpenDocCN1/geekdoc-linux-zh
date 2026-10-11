```
#Change these values for each region
declare REGIONAL_OFFICE="Boston"
declare REGIONAL_MGR="Mary Smith"
let REGIONAL_SALES=1000000

#Display the opening screen
menu1
```

This example is much easier to read because it uses blank lines to break up the code into sections. You add blank lines to your program by inserting a *carriage return* (also known as a **hard return**) on a line that doesn’t contain any text. The easiest way to insert a hard return is to move the cursor to the end of a line of text and press the Enter key. Rather than type text on the line, press the Enter key again. Voilà — a blank line!

# How to Disable a Pesky Instruction

Beware! Bugs can work their way into your program. A bug is an error in your program, and sometimes it’s hard to uncover. Suppose that you write a program to tell your computer to do something, but the computer doesn’t do it. You have a bug in your program! What do you do? The following list provides your choices:

+   - “Scream, ‘I hate computers!’” This technique doesn’t do anything to get your program to work, of course, but it certainly can relieve some of your frustrations.
+   - Test your program to determine which instruction isn’t working. Keep in mind that the computer does what you tell it to do. You’re probably simply given it an incorrect instruction.

You can use comments to disable instructions in your program. Although programmers use a number of techniques to locate bugs in their programs (and I discuss these techniques in depth in Chapter 19), most methods consist of the following basic steps:

+   1. Disable an instruction.
+   2. Test the program.
+   3. Review the results.

You can disable a part of your program by placing the number sign (#) at the beginning of the line that contains the instruction.

Suppose that you run a program (a snippet of which appears in the following example), and for some reason, it displays an incorrect regional sales value. As you inspect your code, you see — and suspect — an instruction that creates a REGIONAL_SALES environment variable that displays a value of 1000000. Can