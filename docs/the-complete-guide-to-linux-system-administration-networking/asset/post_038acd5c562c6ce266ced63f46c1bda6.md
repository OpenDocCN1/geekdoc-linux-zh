
## Table 5-1 Common Regular Expressions in Linux (continued)

| Expression syntax | Meaning of syntax |
|---|---|
| $ | Match text at the end of a line |
| [abc] | Match one of the characters in brackets |
| [^abc] | Exclude all of the characters in brackets |
| \ | Escapes the special meaning of the character that follows it |
| | | (the pipe symbol) Separates alternative choices |
| [n] | Matches n occurrences of the preceding pattern |
| {n,} | Matches at least n occurrences of the preceding pattern |
| {n,m} | Matches at least n occurrences, but not more than m occurrences of the preceding pattern |

The acceptable syntax for a regular expression—and the meaning of some special characters used in them—varies in small but important ways depending on where you are using the expression. Within a shell script, as a parameter to some utilities, within vi, and in other places, you must watch for slight variations in meaning. It's best to test your regular expressions in a way that lets you undo the results (or try them again) as you learn exactly what effect different special characters have. The documentation for different utilities, of course, describes how regular expressions are processed. Once you are familiar with the basic functioning of a regular expression, understanding variations between programs is straightforward.

Walking through a few more examples will help you understand the cryptic descriptions in Table 5-1 and see how regular expressions are constructed. Notice first of all how the same character can have different meanings in different positions. For example, the ^ character generally means "tie this pattern to the beginning of a line," but when placed inside brackets, the ^ means "not" and serves to exclude all characters within the brackets.

Suppose you have a directory full of image files. The name of each file is "reunion" followed by a number. The files are numbered from 00 to 45 (reunion00 to reunion45). You can use several regular expressions to match all of those files in a command such as ls, zip, or gimp (an image editing program):

```
reunion*
```

matches them all. But if some of the files were saved with a capital "R", this doesn't match them all. You can use this:

```
*union*
```

but it's less precise. For example, if you had other files in the same directory with names that included "union," it would match them as well. A more precise pattern is:

```
[Rr]eunion*
```

This matches only files starting with “R” or “r”, followed by “eunion,” followed by any text. Suppose that you only want to include the first twenty images in the pattern. You use this regular expression:

```
[Rr]eunion [01] [0-9]
```

This matches only files that have a 0 or 1 in the first position after “reunion” (or “Reunion”), and files with any digit 0 to 9 in the second position. So files reunion00 to reunion19 match.

If these files have a file extension such as .jpg or .tif, you want to include that in the regular expression. The following matches all 45 files and assumes they have a file extension as well.

```
[Rr]eunion [0-9] [0-9] .jpg
```

A more compact way to express the previous example uses curly braces to indicate repetition of a pattern. Notice that we have [0-9] repeated above. To specify that we want only files with two digits after the word “reunion,” we use this expression:

```
[Rr]eunion [0-9] {2} .jpg
```

Now suppose that your files are named reunion-a through reunion-z. You could match all of these with this expression:

```
reunion- [a-z] .jpg
```

You can use ranges such as 0-9, a-z, and A-Z in any regular expression. If you had mixed up lowercase and capital letters, you might need to revise the above expression to match both:

```
reunion- [a-zA-Z] .jpg
```

If you had multiple letters after the word reunion, you could precisely control how many were matched using a set of curly braces. If you want to match all of these files except reunion-d.jpg, you use this expression:

```
reunion- [^d] .jpg
```

Next, suppose that multiple individuals were saving the image files and used slightly different names. Some use the word “reunion,” but others use “reun” and one person just uses “r”. You can match all of these by using a pipe symbol ( | ) within brackets. Normally, a set of characters in square brackets matches just one character (any one of the characters in brackets), but when a pipe symbol is used, the expression matches alternate sets of characters:

```
r [union|un] - [a-zA-Z] .jpg
```

Notice that the last pipe symbol in the first set of square brackets has nothing after it, because it matches file names such as r-b and r-c.

The examples given here don’t include the ( ^ ) or ( $ ) characters, because those are not useful when matching file names on the command line. Later in this chapter, you’ll see multiple examples of these used with other regular expression characters to find patterns within text files. As you can imagine, regular expressions can become very complex, and every character of the expression is important. Check your work and test your expressions as you learn how they operate in different circumstances.

## MANIPULATING FILES

In this section you learn about command-line utilities that are useful for searching, sorting, reorganizing, and otherwise working with text files. These commands are often used in combination, connected on a single command line by pipe symbols; they also commonly rely on regular expressions, either to select on which files to operate, to select text within the output of a previously executed command, or to match text within a text file. The descriptions in this section use documentation or configuration files on your Linux system to explore the features of each command, but you can use them for any text file you need to process.

![](img/43f64015de86d989e30eff5bb284fb96_228_0.png)

Files created by word-processing or office suite programs such as OpenOffice.org, Word, or Excel are not text files. They contain many special codes that might interfere with processing using the commands described in this section. You can typically export data from these word-processing programs in a text format (using the Save As command, for example). This may make the data accessible for the analysis that you want to do. You may even be able to later import the text information back into the program (formatting information is typically lost). Web pages are written in HTML, which is a text format, so the utilities here may be useful in processing them.

### Searching for Patterns with grep

You have already learned how to use the locate and find commands to locate a file with specific characteristics. To search the contents of files, however, you should use the grep command. grep can rapidly scan files for a pattern that you specify, printing out the lines of text that contain text matching the pattern. You can then take further action on these matching lines of text by using a pipe to connect grep with other filtering commands.

As a simple example of grep, suppose you want to see which shell is used by a certain user account, wilsonr. Rather than opening a user management tool (as discussed in Chapter 11, "Managing Users") or looking at the /etc/passwd file in a text editor, you can enter this command and immediately see the line of /etc/passwd that contains the information you need:

```
$ grep wilson /etc/passwd
wilsonr:x:564:564::/home/wilsonr:/bin/csh
```

The last item in the output line indicates that the current default shell for user wilsonr is the C shell (csh). Note that the grep command searches only for wilson, not for wilsonr. If multiple user names on the system include the string wilson, grep displays a matching line for each one. As a system administrator, you learn when to take shortcuts—on a system with few users, the search pattern "wil" might have worked as well as "wilson." Because anyone can read the /etc/passwd file, you can try this grep example using your own user name as well.
