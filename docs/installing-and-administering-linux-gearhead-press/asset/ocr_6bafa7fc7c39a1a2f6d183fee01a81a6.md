+   6.  Yes. The knights2 group and others have execute permission on the two directories, *jobs* and *work*. The group also has read permission on the *joblog* file. Nicholas presumably has write and execute permissions on his own home directory.

# Chapter 7

+   1.  Redirection, command / variable substitution, wildcard expansion, and command execution.
+   2.  This command lists all the files beginning with any three characters. The fourth character must not be in the range *a* to *z*. Then, any number of characters can follow, after which the second-to-last character must be from 0 through 9. The final character must be *t*.
+   3.  Home directory is */home/quixote*.
+   4.  Home directory is `$HOME`. (Note that this question used single quotes.)
+   5.  Current directory is */home/quixoted/docs*. (Note that pwd is enclosed in back quotes.)
+   6.  Files in this directory are `*`.
+   7.  `aa bb cc /home/quixoted`
+   8.  `*`
+   9.  Standard input (0) is the keyboard; standard output (1) is the screen; standard error (2) is the screen.
+   10. Standard input (0) is a file named *letter*; standard output (1) is handled by the *mail* program; standard error (2) is the screen.
+   11. Standard input (0) is the keyboard; standard output (1) is a file named *newprofile*; standard error (2) is a file named *1* (or *1*, if you would rather. It is sometimes difficult to tell with some of these fonts. At any rate, it was a bit of a trick question: you might have thought that we were clumsily trying to indicate a redirection to standard output and that the ampersand was missing. We were not; we deliberately left the ampersand out).
+   12. `$ cat filea > fileb 2> filec`
+   13. `$ cat filea > fileb 2>&1`
+   14. `$ cat filea > fileb 2> /dev/null`