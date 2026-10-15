# 9.8.3 The Square Brackets

The square brackets match a filename for one character from a set or range of characters.

# EXAMPLE 9.30

```
1 % ls
a.c b.c abc ab3 file1 file2 file3 file4 file5 file10 file11 file12
2 % ls file[123]
file1 file2 file3
3 % ls [A-Za-z][a-z][1-5]
ab3
4 % ls file[0-2]
file10 file11 file12
```

# EXPLANATION

+   1 All the files in the current directory are listed.
+   2 Filenames starting with file and followed by a 1, 2, or 3 are matched and listed.
+   3 Filenames starting with a letter (either uppercase or lowercase) followed by a lowercase letter, and followed by a number between 1 and 5 are matched and listed.
+   4 Filenames starting with file1 and followed by a 0, 1, or 2 are listed.

# 9.8.4 The Curly Braces

The curly braces ({}) match for a character or string of characters in a filename.

# EXAMPLE 9.31

```
1 % ls
a.c b.c abc ab3 ab4 ab5 file1 file2 file3 file4 file5 foo faa fumble
2 % ls f{oo,aa,umble}
foo faa fumble
3 % ls a{,.c,c,b}[3-5]
a.c ab3 ab4 ab5
```

# EXPLANATION

1 All the files in the current directory are listed.
2 Files starting with f and followed by the strings oo, aa, or umble are listed. Spaces inside the curly braces will cause the error message Missing }.
3 Files starting with a followed by ., c, c, or b3, b4, or b5 are listed. (The square brackets can be used inside the curly braces.)