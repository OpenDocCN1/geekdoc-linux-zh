# **The shell expands ambiguous file references**

tip
The shell does the expansion when it processes an ambiguous file reference, not the program that the shell runs. In the examples in this section, the utilities (ls, cat, echo, lpr) never see the ambiguous file references. The shell expands the ambiguous file references and passes a list of ordinary filenames to the utility. In the previous examples, echo demonstrates this fact because it simply displays its arguments; it never displays the ambiguous file reference.

# # THE [ ] SPECIAL CHARACTERS

A pair of brackets surrounding one or more characters causes the shell to match filenames containing the individual characters within the brackets. Whereas memo? matches memo followed by any character, memo[17a] is more restrictive: It matches only memo1, memo7, and memoa. The brackets define a *character class* that includes all the characters within the brackets. (GNU calls this a *character list*; a GNU *character class* is something different.) The shell expands an argument that includes a character-class definition by substituting each member of the character class, one at a time, in place of the brackets and their contents. The shell then passes the list of matching filenames to the program it is calling.

Each character-class definition can replace only a single character within a filename. The brackets and their contents are like a question mark that substitutes only the members of the character class.

The first of the following commands lists the names of all files in the working directory that begin with a, c, i, o, or u. The second command displays the contents of the files named page2.txt, page4.txt, page6.txt, and page8.txt.

```
$ echo [aeiou]*
...

$ less page[2468].txt
...
```

A hyphen within brackets defines a range of characters within a character-class definition. For example, [6-9] represents [6789], [a-z] represents all lowercase letters in English, and [a-zA-Z] represents all letters, both uppercase and lowercase, in English.

The following command lines show three ways to print the files named part0, part1, part2, part3, and part5. Each of these command lines causes the shell to call lpr with five filenames:

```
$ lpr part0 part1 part2 part3 part5

$ lpr part[01235]

$ lpr part[0-35]
```

The first command line explicitly specifies the five filenames. The second and third command lines use ambiguous file references, incorporating character-class definitions. The shell expands the argument on the second command line to include all files that have names beginning with part and ending with any of the characters in the character class. The character class is explicitly defined as 0, 1, 2, 3, and 5. The third