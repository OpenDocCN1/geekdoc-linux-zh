If the element you add is already in the list, you now have two copies of it in the list. Write a shell function named **addenv** that takes two arguments: (1) the name of a shell variable and (2) a string to prepend to the list that is the value of the shell variable only if that string is not already an element of the list. For example, the call

$\quad$ addenv PATH /opt/bin

would add **/opt/bin** to **PATH** only if that pathname is not already in **PATH**. Be sure your solution works even if the shell variable starts out empty. Also make sure you check the list elements carefully. If **/usr/opt/bin** is in **PATH** but **/opt/bin** is not, the example just given should still add **/opt/bin** to **PATH**. (*Hint: You might find this exercise easier to complete if you first write a function* ***locate_field*** *that tells you whether a string is an element in the value of a variable.*)

+   20. Write a function that takes a directory name as an argument and writes to standard output the maximum of the lengths of all filenames in that directory. If the function's argument is not a directory name, write an error message to standard output and exit with nonzero status.

+   21. Modify the function you wrote for exercise 20 to descend all subdirectories of the named directory recursively and to find the maximum length of any filename in that hierarchy.

+   22. Write a function that lists the number of ordinary files, directories, block special files, character special files, FIFOs, and symbolic links in the working directory. Do this in two different ways:
+   a. Use the first letter of the output of `ls -l` to determine a file's type.
+   b. Use the file type condition tests of the `[ [ expression ] ]` syntax to determine a file's type.

+   23. Modify the **quiz** program (page 1072) so that the choices for a question are randomly arranged.