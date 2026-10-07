# Chapter 11: I/O and TRAP Processing

# # CHAPTER 11

# # TEST YOUR THINKING

The projects in this section are meant to have you utilize all of the skills that you have acquired throughout this chapter.The answers to these projects can be found at the companion web site to this book, located at:

http://www.phptr.com/phpptrinteractive/

Visit the Web site periodically to share and discuss your answers.

![](bbox=[0.055, 0.275, 0.145, 0.335])

LAB 11.3

+   1. Modify the "shuffle" script from Exercise 11.2.2 to perform the following:
- If either of the input files does not exist or is not readable, print an error message, don't ask for an output file name, and prompt for another pair of input files.
- If the output file already exists, ask the user whether it is all right to overwrite it (and respond appropriately!).
- If the user presses Ctrl-C, be sure the cursor is positioned at the beginning of the next line before the script exits.
- As written, the program includes all the lines from both files only if the first one has more or an equal number of lines, Modify it so that the output always contains all lines from both files.

+   2. Write the equivalent of the du -k command, which prints the name of each directory under the current one, preceded by the number of kilobytes in all the files in that directory and all its descendants. Hint:You can redirect the output of an ls -l command to a temporary file, and read that file back in to get the file sizes.