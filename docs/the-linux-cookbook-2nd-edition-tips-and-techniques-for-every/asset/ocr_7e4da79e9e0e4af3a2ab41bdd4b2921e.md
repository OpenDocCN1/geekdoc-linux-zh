# 13. Formatting Text

Methods and tools for changing the arrangement or presentation of text are often useful when preparing text for printing. This chapter discusses ways of changing the spacing of text and setting up pages, of underlining and sorting and reversing text, and of numbering lines of text.

Most of these tools are filters (see Recipe 3.2.4 [Redirecting Output to Another Command's Input], page 69).

# 13.1 Spacing Text

These recipes are for changing the spacing of text—the whitespace that exists between words, lines, and paragraphs.

The filters described in this section send output to standard output by default; to save their output to a file, use shell redirection (see Recipe 3.2.2 [Redirecting Output to a File], page 68).

# 13.1.1 Eliminating Extra Spaces in Text

There are a few methods for doing this. To eliminate extra whitespaces within lines of text, use the fmt filter; to eliminate extra whitespace between lines of text, use cat.

# METHOD #1

Use fmt with the -u option to output text with “uniform spacing,” where the space between words is reduced to one space character and the space between sentences is reduced to two space characters.

⇒ To output the file term-paper with uniform spacing, type:

```
$ fmt -u term-paper [RET]
```

# METHOD #2

Use cat with the -s option to “squeeze” multiple adjacent blank lines into one.

⇒ To output the file term-paper with multiple blank lines output as only one blank line, type:

```
$ cat -s term-paper [RET]
```