
# FILENAME GENERATION/Pathname Expansion

Wildcards, globbing When you specify an abbreviated filename that contains *special characters*, also called *metacharacters*, the shell can generate filenames that match the names of existing files. These special characters are also referred to as *wildcards* because they act much as the jokers do in a deck of cards. When one of these characters appears in an argument on the command line, the shell expands that argument in sorted order into a list of filenames and passes the list to the program called by the command line. Filenames that contain these special characters are called *ambiguous file references* because they do not refer to one specific file. The process the shell performs on these filenames is called *pathname expansion* or *globbing*.

Ambiguous file references can quickly refer to a group of files with similar names, saving the effort of typing the names individually. They can also help find a file whose name you do not remember in its entirety. If no filename matches the ambiguous file reference, the shell generally passes the unexpanded reference—special characters and all—to the command. See “Brace Expansion” on page 405 for a technique that generates strings that do not necessarily match filenames.

## The ? Special Character

The question mark (?) is a special character that causes the shell to generate filenames. It matches any single character in the name of an existing file. The following command uses this special character in an argument to the `lpr` utility:

```
$ lpr memo?
```

The shell expands the **memo?** argument and generates a list of files in the working directory that have names composed of **memo** followed by any single character. The shell then passes this list to `lpr`. The `lpr` utility never “knows” the shell generated the filenames it was called with. If no filename matches the ambiguous file reference, the shell passes the string itself (**memo?**) to `lpr` or, if it is set up to do so, passes a null string (see `nullob` on page 402).

The following example uses `ls` first to display the names of all files in the working directory and then to display the filenames that `memo?` matches:

```
$ ls
mem      memo12   memo9    memomax  newmemo5
memo     memo5    memoa    memos
```

```
$ ls memo?
memo5  memo9  memoa  memos
```

The `memo?` ambiguous file reference does not match `mem`, `memo`, `memo12`, `memomax`, or `newmemo5`. You can also use a question mark in the middle of an ambiguous file reference:

```
$ ls
?may4report  may4report  mayqreport  may_.report
mayi4report  mayi4report.79          may.report
```

```
$ ls may?report
may4report  mayqreport  may_.report  may.report
```

You can use `echo` and `ls` to practice generating filenames. The `echo` builtin displays the arguments the shell passes to it:

```
$ echo may?report
may4report  mayqreport  may_.report  may.report
```

The shell first expands the ambiguous file reference into a list of files in the working directory that match the string `may?report`. It then passes this list to `echo`, as though you had entered the list of filenames as arguments to `echo`. The `echo` utility displays the list of filenames.

A question mark does not match a leading period (one that indicates a hidden filename; page 180). When you want to match filenames that begin with a period, you must explicitly include the period in the ambiguous file reference.

## The * Special Character

The asterisk (`*`) performs a function similar to that of the question mark but matches any number of characters, *including zero characters*, in a filename. The following example first shows all files in the working directory and then shows commands that display all the filenames that begin with the string `memo`, end with the string `mo`, and contain the string `alx`:

```
$ ls
anemo      memax12  memo.0612   memoaxl.0620  memorandom  sallymemo
memo       memoa    memoaxl.keep memosally     user.memo
```

```
$ echo memo*
memo memo.0612 memoa memoaxl.0620 memoaxl.keep memorandom memosally
```

```
$ echo *mo
anemo memo sallymemo user.memo
```

```
$ echo *alx*
memaxl memoaxl.0620 memoaxl.keep
```

The ambiguous file reference **memo\*** does not match **amemo**, **mem**, **sallymemo**, or **user.memo**. Like the question mark, an asterisk does *not* match a leading period in a filename.

The **-a** option causes `ls` to display hidden filenames (page 180). The command `echo *` does not display `.` (the working directory), `..` (the parent of the working directory), `.aaa`, or `.profile`. In contrast, the command `echo . *` displays only those four names:

```
$ ls
   aaa  memo.0612  memo.sally  report  sally.0612  saturday  thurs

$ ls -a
   .  ..  aaa  memo.0612  .profile  sally.0612  thurs

$ echo *
   aaa  memo.0612  memo.sally  report  sally.0612  saturday  thurs

$ echo .*
   .  ..  .aaa  .profile
```

In the following example, `.*` does not match **memo.0612**, **private**, **reminder**, or **report**. The `ls .*` command causes `ls` to list **.private** and **.profile** in addition to the contents of the `.` directory (the working directory) and the `..` directory (the parent of the working directory). When called with the same argument, `echo` displays the names of files (including directories) in the working directory that begin with a dot (.) but not the contents of directories.

```
$ ls -a
   .  ..  memo.0612  private  .private  .profile  reminder  report

$ echo .*
   .private  .profile

$ ls .*
   .private  .profile
   .
   ..
   memo.0612  private  reminder  report
   .
   ..

$ echo .*
   .  ..  .private  .profile
```

You can plan to take advantage of ambiguous file references when you establish conventions for naming files. For example, when you end the names of all text files with `.txt`, you can reference that group of files with `*.txt`. The next command uses this convention to send all text files in the working directory to the printer. The ampersand causes `lpr` to run in the background.

```
$ lpr *.txt &
```

> **tip**
> The shell does the expansion when it processes an ambiguous file reference, not the program that the shell runs. In the examples in this section, the utilities (ls, cat, echo, lpr) never see the ambiguous file references. The shell expands the ambiguous file references and passes a list of ordinary filenames to the utility. In the previous examples, echo demonstrates this fact because it simply displays its arguments; it never displays the ambiguous file reference.

## THE [ ] SPECIAL CHARACTERS

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
