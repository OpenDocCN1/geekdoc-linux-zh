# 260 CHAPTER 7 THE SHELL

The following command line prints 39 files, part0 through part38:

$ lpr part[0-9] part[12][0-9] part3[0-8]

The first of the following commands lists the files in the working directory whose names start with a through m. The second lists files whose end with x, or z.

$ echo [a-m]*
...
$ echo *[x-z]*
...

optional When an exclamation point (!) or a caret (^) immediately follows the opening bracket ([]) that defines a character class, the string enclosed by the brackets matches any character not between the brackets. Thus [^sq]* matches any filename that does not begin with t, s, or q.
The following examples show that *ab* matches filenames that do not end with the letters a or b and that [^ab-d]* matches filenames that do not begin with b, c, or d.

$ ls *
aaa ab ac ad ba bb bc cc dd
$ ls *[ab]
ac bc bd cc dd
$ ls *[ab-d]*
aaa ab ac ad

You can cause a character class to match a hyphen (--) or a closing bracket ([]) by placing it immediately before the final bracket.

The next example demonstrates that the ls utility cannot interpret ambiguous file references. The first is called with an argument of ?old. The shell expands ?old into a matching filename, hold, and passes that name to ls. The second command is the same as the first, the ? is quoted (refer to "Special Characters" on page 160). The shell does not recognize this question mark as a special character and passes it to ls. The ls utility generates an error message saying that it cannot find a file named ?old (because there is no file named ?old).

$ ls ?old
hold
$ ls \?old
ls: ?old: No such file or directory

Like most utilities and programs, ls cannot interpret ambiguous file references; that work is to the shell.

# The shell expands ambiguous file references

tip The shell expands the expansion when it processes an file reference, not the program that the shell runs. In this section, the utilities (ls, cat, echo, lpr) never see the ambiguous file references. The shell expands the ambiguous file reference and passes a list of ordinary filenames to the utility. In the previous examples, echo shows this to be true because it displays its arguments; it never displays the ambiguous file reference.