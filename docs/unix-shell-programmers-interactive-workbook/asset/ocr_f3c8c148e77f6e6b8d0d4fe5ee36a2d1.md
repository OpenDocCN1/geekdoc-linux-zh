# Chapter 4: Simple Variables 179

d) What prevents grep from printing variables that contain RAND-DOM= as part of their value?

e) What prevents grep from printing out a variable named RAND-DOMIZE?

Assign the value OH to the variable state, and verify that state is initialized, but that city and zip are not.

+   f) What command line(s) did you use?

> You can use multiple -e options to get grep to search for multiple strings. Each -e is followed by one of the strings you want to find.

There is essentially no difference between a variable that is uninitialized and one that is initialized to an empty string, but you can see a difference if you try:

Uninitialize a variable y (just to be sure your answers agree with mine), and print a reference to it immediately preceded by the letter X and immediately followed by the letter Z.

+   g) What command line did you use, and what was the output?

Assign the value 123 to y, and print a reference to y surrounded by the characters X and Z again.