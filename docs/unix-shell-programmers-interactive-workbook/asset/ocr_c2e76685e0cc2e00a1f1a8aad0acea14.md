# Chapter 10: Patterns, Expansions, and Substitutions 441

a.b b.c c.d d.e
**[10015]:**

That is, two question marks print as two question marks, but three questions expand to all the file names with exactly three characters in them. You might expect that two question marks should expand to nothing because there are no file names that match that pattern. However, think about the difference between the following two ls commands:

```
ls
ls "??"
```

The first one is what you would get if you typed ls ?? with no twocharacter file names in the directory and the shell substituted nothing; ls would print the names of all files in the directory. The second one is what you get with the left shell's actual behavior. The double question mark is passed as a parameter to the ls command, which prints out the following-error message:

```
ls: ??: not found
```

There may be situations where the "expected" behavior would be better, but this is the way the shell works.

Answer:The outputs look like the following:
**[1014]: print ??\**
a.b b.c c.d d.e
**[1015]: print ??e**
d.e.
**[1016]:**

Both patterns generate lists of three-character file names, but the last one has added the constraint that the file name must end in e. A pattern equivalent to the last one would be ???*e, but you can't use it for parameter expansion because the shell interprets the ampersand to mean "run the command to left asynchronously" as discussed in Chapter 2,