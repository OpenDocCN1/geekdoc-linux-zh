
## What Are Regular Expressions?

NEW TERM Regular expressions are patterns that use special syntax to match strings (usually in text in files, unless your search is for filenames). There are also extended regular expressions that can use additional operators in the search patterns. The difference, important for syntax, should not deter you from learning how to construct patterns that accurately match your desired search targets. This is important if you're looking for text in files and critical if you're performing potentially dangerous tasks, such as multiple file deletions across your system.

You can build an infinite number of regular expressions using only a small subset of pattern characters. Table 5.1 contains a short list of some of these characters. You should be familiar with at least one (the asterisk) from the previous examples.

**TABLE 5.1 COMMON REGULAR EXPRESSIONS**

| Expression | Matching |
|---|---|
| * | Any character |
| ? or . | A single character |
| {x} | Preceding character x times |
| {x,y} | Preceding character at least x times but no more than y |
| {x,} | Preceding character at least x times |
| (xxx)|(XXX) | String xxx or XXX |
| [xxx] or [x-x] | A character in a range of characters |
| [XYZ]+ | X, Y, or Z at least once |
| \x | A character such as ? or \ |
| ^pattern | pattern at the beginning of a line |
| $pattern | pattern at the end of a line |

This is not a comprehensive list of pattern characters. For more details, you can read the ed manual page (the ed command is discussed in Hour 14, “Text Processing”). For now, try several simple examples using different patterns.

The asterisk is useful for finding matches to all characters. For example, if you want to find all the text files in your directory with an extension of .txt, you can use the following:

```
# ls *.txt
14days.txt 96hours.txt datalog.txt datebook.txt day67.txt
```

But suppose you want a list of all the files in your directory with numbers in the file-name? You can try to string multiple searches on the ls command line, like this:

```
# ls *0* *1* *2* *3* *4* *5* *6* *7* *8* *9*
08100097.db      14days.txt       backup001.file   phonelog.111597
08100097.db      32days.msg       day67.txt        phonelog.111597
08100097.db      32days.msg       day67.txt        phonelog.111597
08100097.db      96hours.txt      message.76
08100097.db      96hours.txt      message.76
14days.txt       backup001.file   phonelog.111597
```

Obviously, this is not the result you want because the multiple searches have printed duplicate filenames. To find exactly what you want, use a regular expression that tells ls to list any file that has a number appearing in the file's name, as follows:

```
# ls *{0123456789}*
0001file.0009    32days.msg       day67.txt
08100097.db      96hours.txt      message.76
14days.txt       backup001.file   phonelog.111597
```

This shows all the files containing numbers in the filename because you specify a range of characters or, in this case, numbers in your search pattern. You can also use a regular expression shorthand to build a shorter expression to do the same thing, for example:

```
# ls *{0-9}*
0001file.0009    32days.msg       day67.txt
08100097.db      96hours.txt      message.76
14days.txt       backup001.file   phonelog.111597
```

How you specify your pattern characters in your expression is important. If you only want a list of files ending in a number, you can use the following:

```
# ls *{0-9}
0001file.0009    message.76       phonelog.111597
```

If you only want a list of files beginning with a number, you can use this:

```
# ls [0-9]*
0001file.0009 08100097.db 14days.txt 32days.msg 96hours.txt
```

Here's a fun exercise: What if you want to list those files with numbers only inside or on both ends of a filename? Try these:

```
# ls *[-a-z][0-9]*
backup001.file day67.txt
# ls [0-9]*[-a-z]*[0-9]
0001file.0009
```

Finally, how do you match patterns when the pattern you're looking for contains a pattern-matching character? Easy! Use the backslash to escape the character, for example:

```
# ls *\?*
cathy?.message
```

As you can see, using regular expressions can take some practice, but your efforts are well rewarded. Try experimenting with different expressions to see if you can come up with results similar to the examples shown in this section.

## Searching Inside Files with the grep Commands

This section introduces you to the family of grep commands. You'll learn about grep, egrep, and fgrep. In order to use these commands, you should know how to use some of the pattern-matching techniques already discussed. You'll use these commands to search through files and extract text. Each of these programs works by searching each line in a file. You can search single files or a range of files.

Each of the grep commands is basically the same and has nearly 20 different command-line options. The only real difference is that egrep uses a slightly different syntax for its pattern matching, whereas fgrep uses fixed strings. You'll see examples of each program and use some of the common options. For specific details about the pattern-matching capabilities of these programs, see the grep manual page.

To show you the difference in each program's search pattern syntax, I'll look for different patterns in Matt Welsh's Linux Basic Installation Guide (available at http://metalab.unc.edu/LDP or on your OpenLinux system in the /usr/doc/LDP directory). For example, if you want to find all the lines in the guide that begin with a number, use the following syntax:

```
# grep '^[0-9]' guide.txt
1 Introduction to Linux 1
2 Obtaining and Installing Linux 40
3 Linux Tutorial 85
4 System Administration 137
...
# egrep '^[0-9]' guide.txt
1 Introduction to Linux 1
2 Obtaining and Installing Linux 40
3 Linux Tutorial 85
4 System Administration 137
...
# fgrep '^[0-9]' guide.txt
```

You can see that grep and egrep returned a search (I deleted all the output except the first four lines). Note, however, that fgrep can not handle regular expressions. You must use fixed patterns or strings with the fgrep command, for example:

```
# fgrep friend guide.txt
```

large extent by the window manager. This friendly program is in copy Linux from a friend who may already have the software, or share (Unfortunately, the system was being unfriendly.)

Now use egrep to try searching for the pattern of the letter (b) in the file:

```
# egrep "\[(b)\]" guide.txt
```

(see Section 1.8 for a list of compatible boards), or (b) there is an connect to the network, or (b) you have a 'dynamic' IP address,

You see that exactly two lines in the file match (b). See what happens when you search with grep:

```
# grep "\(b\)" guide.txt
```

This is version 2.2.2 of the book, "Linux Installation and Getting to PostScript printers. This document was generated by a set of tools from LaTeX source, so there may be a number of formatting problems. This is not the "official" version of the book! Please see ...

Whoa! Not exactly what you wanted, is it? As you can see, grep does not use the same syntax as the egrep command. But you can use a simpler approach:

```
# grep "(b)" guide.txt
```

(see Section 1.8 for a list of compatible boards), or (b) there is an connect to the network, or (b) you have a 'dynamic' IP address,

This pattern works with grep and fgrep. If you try this pattern with egrep, you get the same results as if you tried extended regular expressions with grep (each line with a (b)).

Each grep program accepts nearly the same set of command-line options. One popular option is -n, or line numbering. This is handy because you see which lines in the file contain matches. This example works for each grep program:

```
# egrep -n "friend" guide.txt
```

1242:large extent by the window manager. This friendly program is in 1942:copy Linux from a friend who may already have the software, or 5161:(Unfortunately, the system was being unfriendly.)

You can see that matches were on lines 1242, 1942, and 5161. Another feature of these programs is that you don't have to retype your patterns each time you want to search. As a simple example, if you need to repeatedly search files for different words, you can put these into a file for grep to use. First, create a text file and then use the -f option to specify the file, as follows:
