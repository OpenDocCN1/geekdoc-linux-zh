# Chapter 29 ♦ Programming Tools and Utilities 795

The sixth rule defines a target named realclean. It uses the fifth rule as one of its dependencies. This causes make to build the clean target and then to remove the editor binary.

Here is where make's value becomes evident: Ordinarily, if you tried to build editor using the command from the second line, gcc would complain loudly and ceremoniously if the dependencies did not exist. Make, on the other hand, after determining that editor requires these files, first verifies that they exist, and if they don't, executes the commands to create them.

After creating dependencies, make returns to the first rule to create the editor executable. Of course, if the dependencies for the components, editor.c, screen.c, or keyboard.c, do't exist, make gives up because it lacks targets named, in this case, editor.c, screen.c, or keyboard.c (that is, no rules defined in the makefile for editor.c, screen.c, and keyboard.c).

All well and good, you are probably thinking, how does make know when to build or rebuild a file? The answer is simple: if a specified target does not exist in a place where make can find it, make builds or rebuilds it. If the target exists, make compares the timestamp on the target to the timestamp in the dependencies. If one or more of the dependencies is newer than the target, make rebuilds it, assuming that the newer dependency implies some code change that must be incorporated into the target.

# Library Utilities

Programming libraries are collections of code that can be reused across multiple software projects. Libraries are a classic example of development's ardent goal: reuse. They collect frequently used programming routines and utility code into a single location.

The standard C libraries, for example, contain hundreds of frequently used routines, such as the output printf() and the input function getchar() that would be tiresome to rewrite each time you create a new program. By code reuse and programmer convenience, however, libraries provide a great deal of thoroughly debugged and well-tested code, such as routines for network programming, graphics handling, data manipulation, and system calls.

You need to know the tools at your disposal for creating, maintaining, and managing programming libraries. There are two types of libraries: static and shared:

+   * Static libraries — Static libraries are specially formatted libraries that contain object files, called modules or members, of reusable, precompiled code. They are stored in a special format along with a table or map that links symbol