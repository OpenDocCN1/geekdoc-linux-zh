# Wildcards and Regular Expressions

4. Variations are possible, too. I could use wildcards to list all files or directories that end with the letter: s:

```
% echo "s"
Archives News
```

What happens if I try the same command using the `ls` command rather than the echo command:

```
% ls -CF "s"
Archives:
Interleaf.story  Tartan.story.Z  nextstep.txt
Opus.interactive.txt  rae.assist.infoworld.Z
```

```
News:
lists.usenet  usenet.alt
```

Using the is here makes UNIX think I want to list two directories, not just the names of the two files. This is where the `-d` flag from `ls` could be helpful to force a listing of the directories rather than their contents.

5. Notice that, in the News directory, I have three files with the word usenet in their names. The wildcard pattern `usenet*` would match two of them, and `*usenet` would match one. A value of the `*` wildcard is to match zero or more characters, so the pattern `*usenet*` will match all three.

```
% echo "*usenet"
News/lists.usenet usenet.1 News/usenet.alt
```

Also notice that wildcards can be embedded in a filename or pathname. In this example, I match a single character? To see how this I was interested in files in the News directory.

6. Could see how this can be helpful, to move into a different directory, OWL on my system.

```
% ls -CF
Student.config owl.c owl.o
Wordlist/ owl.data simple.editor.c
owl*h simple.editor.o
```

If I request \*, which files will be listed?

```
% echo "*"
owl.c owl.data owl.h.o
```

What do I do if I am only interested in the source, header, and object files, which are indicated by a .c, .h, or .o. Using a wildcard that matches zero or more letters won't work; I don't want to see `owl` or `owl.data`. One possibility would be to use the pattern `owl.*` (by adding the period, I can eliminate the owl file itself).
What I really want, however, is to be able to specify all files that start with the four characters owl* and have exactly one character. This is a situation in which the ? wildcard works:

![](bbox=[0.883, 0.269, 0.936, 0.313])