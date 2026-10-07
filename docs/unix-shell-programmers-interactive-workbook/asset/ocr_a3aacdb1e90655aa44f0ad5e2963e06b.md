# Lab 10.1: Patterns

There are also exactly nine files in the directory. The idea is to see that the asterisk pattern in the for command generates a list of all the file names in the directory. The case statement matches each file name to exactly one of the patterns shown there, resulting in one line of output for each file.

+   g) What is the value of f the first time through the loop?
Answer: It's a.

This file name matches two of the patterns in the case statement—the first and the last ones—but the first is the one that gets printed. Once it reaches the double-semicolon after that print command, the shell terminates execution of the case statement and does not try to match the a to any of the other patterns.

+   h) What would print if the print command's message was not in queries?
Answer:The output for just the first iteration would look like the following:
atMatches a.b.

As you can see, the at prints the letter t instead of as a <Tab>, and the names of all files that match the a* pattern are printed instead of the characters a*.

![](bbox=[0.195, 0.574, 0.303, 0.638])

> Putting quotes (either single or double) characters makes the shell treat the characters as a string, even if they contain pattern characters, such as asterisks.
files a.b and b.c?
Answer:The output lines for these two files look like the following:
a.b Matches a*.
b.c Has a dot in it.

Both files have dots and bs in their names, yet they match different patterns because a* is the first pattern that a.b matches in the case statement, whereas *.* is the first pattern that b.c matches. If you changed the order of the legs of the case statement, you would get different outputs.