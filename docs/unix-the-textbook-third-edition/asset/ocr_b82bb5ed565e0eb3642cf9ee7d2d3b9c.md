b. How would you test that this environment variable is actually implementing the user option change, and not what is in the ~/.exrc or ~/.vimrc files?

c. What syntax would you use for the SETENV command to change more than one user option in the editors?

d. Are these changes in the EXINIT variable persistent through all vi, vim, and gvim sessions? If you log out and log back in to the system, does EXINIT still contain the changes and additions you made to it? Why or why not?

10. Give the exact syntax of a vi substitute command line that only replaces every instance of the discrete word ate on all the lines of a file with the word ion, where the file has some words that end in the string ate.

11. Give the exact syntax of a vim substitute command line that interactively searches and substitutes the word cool for the word cold on all the lines of a file, where there are several widely separated instances of the word cold in the file.

12. Take the following map command for creating a skeleton C program template, and place it in your ~/.exrc file:
map #3 "^[^#include <stdio.h> ^Mmain(argc, argv) ^M int argc;^M char *argv[];^M(^M)^M^M[

where:
^[ stands for pressing <Ctrl+v> and then <Esc>
^M stands for pressing <Ctrl+v> and then the <Enter> key

As stated in the text, the relative number of spaces in the map command definition controls the indentation of the skeleton construct. Also, the ^M entries put each of the skeleton construct components on a new line.

a. Make sure that the relative indentation of the header components and other parts of the skeleton is correct.

b. Add #include <stderr.h>, #include <stdlib.h>, and #include <string.h> as header information to the skeleton.

c. Run the map command in a blank vi buffer and test it.

13. To practice with the command line window to reuse any previous searches in your search history, use vim to edit the file multiline you created in Practice Session 3.4. Then search for the words engineers, system administrators, web servers, scientists, networking, and mathematicians, one search at a time, starting at the first character in the buffer. Open a command line window on your search history. Modify the search commands in the history of searches for scientists, networking, and mathematicians to be commands that substitute