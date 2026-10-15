
You need to learn two basic wildcards: * acts as a match for any number and sequence of characters, and ? acts as a match for any single character. In the broadest sense, a lone * acts as a match for all files in the current directory (in other words, ls * is identical to ls), whereas a single ? acts as a match for all one-character-long filenames in a directory (for instance, ls ?, which will list only those filenames that are one character long).

- 1. To experiment with wildcards, it’s easiest to use the echo command. Recall that echo repeats anything given to it, but—and here’s the secret to its value—the shell interprets anything that is entered before echo sees it. That is, the * is expanded before the shell hands the arguments over to the command:

Click here to view code image

```
$ echo *
Archives InfoWorld Mail News OWL bin bitnet.mailin g-lists.Z
drop.text.hqx keylime.pie src temp testme
```

Using the * wildcard enables you to easily reference all files in the directory.

- 2. A wildcard is even more helpful than the example suggests because it can be embedded in the middle of a word or otherwise used to limit the number of matches. To see all files that began with the letter t, use t*:

```
$ echo t*
temp testme
```

- 3. Variations are possible, too. You could use wildcards to list all files or directories that end with the letter s:

```
$ echo *s
Archives News
```

Watch what happens if I try the same command using the ls command rather than the echo command:

Click here to view code image

```
$ ls -F *s
Archives:
Interleaf.story Tartan.story.Z nextstep.txt.Z
Opus.story interactive.txt.Z rae.assist.infoworld.Z

News:
mailing.lists.usenet usenet.l usenet.alt
```

Using the ls command here makes the shell think I want to list the contents of the two directories, not just the directory entries themselves. This is where I need to use the -a flag to ls to force a listing of the directories rather than of their contents.

- 4. Notice that, in the News directory, I have three files with the word usenet somewhere in their names. The wildcard pattern usenet* would match two of the files, and *usenet would match one. A valuable aspect of the * wildcard is that it can match zero or more characters, so the pattern *usenet* will match all three filenames:

Click here to view code image

```
$ echo News/*usenet*
```

News/mailing.lists.usenet News/usenet.l1 News/usenet.alt

Also notice that wildcards can be embedded in a filename or pathname. In this example, I specified that I was only interested in files in the News directory.

## 5. Can you match a single character? To see how this can be helpful, it’s time to move into a different directory, such as OWL on my system:

Click here to view code image

```
% cd OWL
% ls -F
Student.config    owl.c       owl.o
WordMap/          owl.data    simple.editor.c
owl*              owl.h       simple.editor.o
```

If I request owl*, which files will be listed?

Click here to view code image

```
% echo owl*
owl owl.c owl.data owl.h owl.o
```

What do I do if I am interested only in the source, header, and object files, which are here indicated by a .c, .h, or .o suffix? Using a wildcard that matches zero or more letters won’t work; I don’t want to see owl or owl.data. One possibility would be to use the pattern owl.* (because by adding the period, I can eliminate the owl file itself). What I really want, however, is to be able to specify all files that start with the four characters owl. and have exactly one more character. This is a situation in which the ? wildcard works:

```
% echo owl.?
owl.c owl.h owl.o
```

Because no files have exactly one letter following the three letters owl, watch what happens when I specify owl? as the pattern:

```
% echo owl?
echo: No match.
```

## 6. You can use even more sophisticated wildcards. Next you’ll learn about some of them so you can get a sense of what can be accomplished on the command line.

A pair of square brackets denotes a range of characters, which can be either explicitly listed or indicated as a range with a dash between them I can explicitly list the letters of interest by listing them all tucked neatly into a pair of square brackets, as shown here:

Click here to view code image

```
% ls -ld [abkost]*
-rw-rw-- 1 taylor 126 Dec 3 16:34 awkscript
-rw-rw-- 1 taylor 165 Dec 3 16:42 bigfiles
drwx--- 2 taylor 512 Oct 13 10:45 bin/
-rw-rw-- 1 taylor 12556 Nov 16 09:49 keylime.pie
-rw-rw-- 1 taylor 8729 Dec 2 21:19 owl.c
-rw-rw-- 1 taylor 199 Dec 3 16:11 sample
-rw-rw-- 1 taylor 207 Dec 3 16:11 sample2
drwx--- 2 taylor 512 Oct 13 10:45 src/
drwxrwx- 2 taylor 512 Nov 8 22:20 temp/
```
