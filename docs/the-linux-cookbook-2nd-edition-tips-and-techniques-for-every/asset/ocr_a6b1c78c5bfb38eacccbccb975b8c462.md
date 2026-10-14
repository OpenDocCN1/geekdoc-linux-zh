# METHOD #3

You can combine both of these commands to output text with multiple adjacent lines removed and with uniform spacing between words. The following example sends the output of the combined commands to less so that it can be perused on the screen.

⇒ To peruse the text file term-paper with multiple blank lines removed and giving the text uniform spacing between words, type:

```
$ cat -s term-paper | fmt -u | less [RET]
```

Notice that in this example, both fmt and less worked on their standard input instead of on a file—the standard output of cat (the contents of term-paper with extra blank lines squeezed out) was passed to the standard input of fmt; its standard output (the space-squeezed term-paper, now with uniform spacing) was sent to the standard input of less, which displayed it on the screen.

# 13.1.2 Single-Spacing Text

There are many methods for single-spacing text. These are my favorites.

# METHOD #1

To remove all empty lines from text output, use grep with the regular expression "." to match any character, and will therefore match any line that isn’t empty (see Recipe 14.3 [Matching Patterns of Text], page 335). You can then redirect this output to a file, or pipe it to other commands. The original file is not altered.

⇒ To output all non-empty lines from the file term-paper, type:

```
$ grep . term-paper [RET]
```

This command outputs all lines that are not empty—so lines containing only non-printing characters, such as spaces and tabs, will still be output.

# METHOD #2

To remove from the output all empty lines, and all lines that consist of only space characters, use grep with "[^ ]." as the regexp to search for.

⇒ To output only the lines from the file term-paper that contain more than just space characters, type:

```
$ grep '[^ ].' term-paper [RET]
```