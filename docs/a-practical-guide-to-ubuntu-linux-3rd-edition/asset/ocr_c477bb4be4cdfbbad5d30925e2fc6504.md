+   a. With both input and output redirected.
+   
+   b. With only input redirected.
+   
+   c. With only output redirected.
+   
+   d. Within a pipe.
+   
+   In which of the preceding cases is grep used as a filter?
+   
+   9. Explain the following error message. Which filenames would a subsequent ls display?
+   
+       $ ls
+   
+       abc abd abe abf abg abh
+   
+       $ rm abc ab\*
+   
+       rm: cannot remove 'abc': No such file or directory

# ## ADVANCED EXERCISES

+   10. When you use the redirect output symbol (>) with a command, the shell creates the output file immediately, before the command is executed. Demonstrate that this is true.
+   
+   11. In experimenting with shell variables, Max accidentally deletes his PATH variable. He decides he does not need the PATH variable. Discuss some of the problems he may soon encounter and explain the reasons for these problems. How could he easily return PATH to its original value?
+   
+   12. Assume your permissions allow you to write to a file but not to delete it.
+   
+       a. Give a command to empty the file without invoking an editor.
+   
+       b. Explain how you might have permission to modify a file that you cannot delete.
+   
+   13. If you accidentally create a filename that contains a nonprinting character, such as a CONTROL character, how can you remove the file?
+   
+   14. Why does the noclobber variable not protect you from overwriting an existing file with cp or mv?
+   
+   15. Why do command names and filenames usually not have embedded SPACES? How would you create a filename containing a SPACE? How would you remove it? (This is a thought exercise, not recommended practice. If you want to experiment, create and work in a directory that contains only your experimental file.)
+   
+   16. Create a file named answer and give the following command:
+   
+       $ > answers.0102 < answer cat
+   
+       Explain what the command does and why. What is a more conventional way of expressing this command?