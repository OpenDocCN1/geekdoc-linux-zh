
⇒ To output the file zim.bibliography with all underlined characters removed but all underlines kept, type:

```
$ col -b < zim.bibliography [RET]
```

NOTES: This is also good for removing overstrikes from text, where a character such as "X" is used in place of an underline.

## 13.10 Reversing Text

These recipes show ways to reverse the order of lines of text, and to reverse the order of characters on each line.

### 13.10.1 Reversing Lines of Text

The tac command is similar to cat, but it outputs text in reverse order. That is, it outputs the last line of its input first, and the first line of its input last.

There is another difference—tac works on records, sections of text with separator strings, instead of lines of text. Its default separator string is the linebreak character, so by default tac outputs files in line-for-line reverse order.

⇒ To output the file prizes in line-for-line reverse order, type:

```
$ tac prizes [RET]
```

Specify a different separator with the -s option. This is often useful when specifying non-printing characters, such as formfeeds. To specify such a character, use the ANSI-C method of quoting (see Recipe 3.1.3 [Quoting Reserved Characters], page 56).

⇒ To output prizes in page-for-page reverse order, type:

```
$ tac -s $'\f' prizes [RET]
```

The preceding example uses the formfeed, or page break, character as the delimiter, so it outputs the file prizes in page-for-page reverse order, with the last page output first.

Use the -r option to use a regular expression for the separator string (see Recipe 14.3 [Regular Expressions—Matching Patterns of Text], page 335). You can build regular expressions to output text in word-for-word and character-for-character reverse order:

⇒ Here are two ways to use this:

- To output prizes in word-for-word reverse order, type:

```
$ tac -r -s '[^-a-ZA-Z0-9-]' prizes [RET]
```

- To output **prizes** in character-for-character reverse order, type:

```
$ tac -r -s '.'
' [RET]
' prizes [RET]
```

### 13.10.2 Reversing the Characters on Lines

To reverse the order of characters on each *line*, use **rev**. It takes as input the name of the file to reverse, and it writes to the standard output. With no options, it reads from standard input.

⇒ To output **prizes** with the characters on each line reversed, type:

```
$ rev prizes [RET]
```

## 14. Searching Text

It’s quite common to search through text for a given sequence of characters (such as a word or phrase), called a *string*, or even for a pattern describing a *set* of such strings; this chapter contains recipes for doing these kind of things.

### 14.1 Searching Text for a Word

The primary tool used for searching through text is `grep`, whose frog-like name is often used as a verb to describe the process of searching through text, as in “Did you `grep` the list for his name?” It outputs lines of its input that contain a given string or pattern.

To search for a word, give that word as the first argument. By default, `grep` searches standard input; give the name of a file to search as the second argument.

- ⇒ To output lines in the file `catalog` containing the word “CD,” type:
  $ grep CD catalog RET

Use the `-i` option to ignore the case when looking for matches.

- ⇒ To output lines in the file `catalog` containing “cd,” regardless of case, type:
  $ grep -i cd catalog RET

This search matches any lines in `catalog` where the pattern “cd” is found, regardless of case. So it will match lines containing “CD” and “cd,” as well as any other variation in case, like “Cd.”

However, this search also matches lines containing, say, the word “anecdote,” as well as words like “CDROM” or “CDR,” because `grep` matches patterns wherever they occur on a line.

To specify that only whole *words* should count as matches, use `grep` with the `-w` option. This ignores matches that occur in the middle of a word. Only entire words will count as a pattern match, which means the pattern’s location must meet two criteria: One, it must be either at the beginning of the line, or be directly preceded by non-letters and non-digits; and two, it must either be directly followed by non-letters or non-digits, or be at the end of the line.

- ⇒ To output lines in the file `catalog` containing the word “CD,” type:
  $ grep -w CD catalog RET

1 The origin of its name is explained in Recipe 14.3 [Regular Expressions—Matching Patterns of Text], page 335, where its advanced usage is discussed.
