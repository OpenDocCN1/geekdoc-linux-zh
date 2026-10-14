
## 15. Searching Text

It's quite common to search through text for a given sequence of characters (such as a word or phrase), called a *string*, or even for a pattern describing a *set* of such strings; this chapter contains recipes for doing these kind of things.

### 15.1 Searching for a Word or Phrase
Finding a word or phrase.

### 15.2 Regular Expressions—Matching Text Patterns
How to specify and find patterns.

### 15.3 Searching More than Plain Text Files
Searching in other than text files.

### 15.4 Outputting the Context of a Search
Searching in a certain context.

### 15.5 Searching and Replacing Text
Searching and replacing text.

### 15.6 Searching Text in Emacs
Searching in Emacs.

### 15.7 Searching Text in Less
Searching in less.

## 15.1 Searching for a Word or Phrase

The primary command used for searching through text is the rather froglike-sounding tool called grep (the origin of its name is explained in Regular Expressions—Matching Text Patterns, where its advanced usage is discussed). It outputs lines of its input that contain a given string or pattern.

To search for a word, give that word as the first argument. By default, grep searches standard input; give the name of a file to search as the second argument.

- To output lines in the file `catalog` containing the word `CD`, type:

```
$ grep CD catalog RET
```

To search for a phrase, specify it in quotes.

- To output lines in the file `catalog` containing the word `Compact Disc`, type:

```
$ grep 'Compact Disc' catalog RET
```

The preceding example outputs all lines in the file `catalog` that contain the exact string `Compact Disc`; it will not match, however, lines containing `compact disc` or any other variation on the case

of letters in the search pattern. Use the `-i` option to specify that matches are to be made regardless of case.

- To output lines in the file `catalog` containing the string `compact disc` regardless of the case of its letters, type:

```
$ grep -i 'compact disc' catalog RET
```

This command outputs lines in the file `catalog` containing any variation of the pattern `compact disc`, including `Compact Disc`, `COMPACT DISC`, and `comPact dIsC`.

One thing to keep in mind is that grep only matches patterns that appear on a single line, so in the preceding example, if one line in `catalog` ends with the word `compact` and the next begins with `disc`, grep will not match either line. There is a way around this with grep (see section Finding Phrases Regardless of Spacing), or you can search the text in Emacs (see section Searching for a Phrase in Emacs).

You can specify more than one file to search. When you specify multiple files, each match that grep outputs is preceded by the name of the file it's in (and you can suppress this with the `-h` option.)

- To output lines in all of the files in the current directory containing the word `CD`, type:

```
$ grep CD * RET
```

- To output lines in all of the `.txt` files in the `~/doc` directory containing the word `CD`, suppressing the listing of file names in the output, type:

```
$ grep -h CD ~/doc/*.txt RET
```

Use the `-r` option to search a given directory recursively, searching all subdirectories it contains.

- To output lines containing the word `CD` in all of the `.txt` files in the `~/doc` directory and in all of its subdirectories, type:

```
$ grep -r CD ~/doc/*.txt RET
```

*NOTE:* There are more complex things you can search for than simple strings, as will be explained in the next section.

## 15.2 Regular Expressions---Matching Text Patterns

In addition to word and phrase searches, you can use grep to search for complex text patterns called regular expressions. A regular expression—or "regexp"—is a text string of special characters that specifies a set of patterns to match.

Technically speaking, the word or phrase patterns described in the previous section are regular expressions—just very simple ones. In a regular expression, most characters—including letters and numbers—represent themselves. For example, the regexp pattern `1` matches the string `1`, and the pattern `bee` matches the string `bee`.

There are a number of reserved characters called metacharacters that don't represent themselves in a regular expression, but have a special meaning that is used to build complex patterns. These metacharacters are as follows: . , * , [ , ] , ^ , $ , and \.

To specify one of these literal characters in a regular expression, precede the character with a `\`.

- To output lines in the file `catalog` that contain a `$` character, type:

```
$ grep '\$' catalog RET
```

- To output lines in the file `catalog` that contain the string `$1.99`, type:

```
$ grep '\$1\.99' catalog RET
```

- To output lines in the file `catalog` that contain a `\` character, type:

```
$ grep '\\' catalog RET
```

The following table describes the special meanings of the metacharacters and gives examples of their usage.

| METACHARACTER | MEANING |
| --- | --- |
| . | Matches any one character, with the exception of the newline character. For example, `.` matches `a`, `1`, `?`, `.` (a literal period character), and so forth. |
| * | Matches the preceding regexp zero or more times. For example, `-*` matches `-`, `--`, `---`, `--------`, and so forth. Now imagine a line of text with a million `-` characters somewhere in it, all marching off across the horizon, up into the blue sky, and through the clouds. A million `-` characters in a row. This pattern would match it. Now think of the same long parade, but it's a million and one `-` characters—it matches that, too. |
| [] | Encloses a character set, and matches any member of the set—for example, `[abc]` matches either `a`, `b`, or `c`. In addition, the |
