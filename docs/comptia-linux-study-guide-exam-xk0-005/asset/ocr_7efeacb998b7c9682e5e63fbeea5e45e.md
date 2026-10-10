# **Listing 4.42:** Using a **gawk** program file

```
$ cat cake.txt
Christine likes chocolate cake.
Rich likes lemon cake.
Tim only likes yellow cake.
Samatha does not like cake.
$
$ cat script.gawk
{if ($4=="cake.")
{$5="donuts"; print $0}}
else if ($5=="cake.")
{$5="donuts"; print $0}}
$
$ gawk -f script.gawk cake.txt
Christine likes chocolate donuts
Rich likes lemon donuts
Tim only likes yellow donuts
Samatha does not like donuts
$
```

In Listing 4.42, a more complex if structure statement is written using the **gawk** programming language and saved to a file, `script.gawk`. This script not only employs an `if` statement, it also incorporates an `else if` structure. Notice also that no single quotation marks are needed when the **gawk** program is stored in a file. Using the -f switch, the program is enacted on the `cake.txt` file, and the appropriate word is changed in every line.

# # Summary

Being able to process data to make agile decisions is important for administering your Linux system. There are many Linux structures and tools, which can help you in uncovering the information you need.

This chapter's purpose was to continue to improve your Linux command-line tool belt. The tools and structures added in this chapter will allow you to search and analyze text in order to uncover knowledge in an efficient manner.