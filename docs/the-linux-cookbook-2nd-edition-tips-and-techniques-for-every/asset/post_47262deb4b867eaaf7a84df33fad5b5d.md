
# METHOD #2

The other way to number lines is to use cat with one of the following two options: The -n option numbers each line of its input text, while the -b option only numbers non-blank lines.

⇒ Here are two ways to use this.

- To peruse the text file citations with each line of the file numbered, type:

```
$ cat -n citations | less [RET]
```

- To peruse the text file citations with each non-blank line of the file numbered, type:

```
$ cat -b citations | less [RET]
```

In the preceding examples, output from cat is piped to less for perusal; the original file is not altered.

To take an input file, number its lines, and then write the line-numbered version to a new file, send the standard output of the cat command to the new file to write.

⇒ To write a line-numbered version of file report to file report.lines, type:

```
$ cat -n report > report.lines [RET]
```

## 13.9 Underlining Text

In the days of typewriters, text that was meant to be set in an italicized font was denoted by underlining the text with underscore characters. Today, it's common practice to denote an italicized word in plain text by typing an underscore character (_) just before and after a word in a text file, like "_this_". I call this etext-style underlining.

Another method of underlining text is overstrike-style or backspace underlining, where each character to underline is immediately followed by a backspace character ("Control-H") and an underscore character (_).

Special ways to view underlined text are described in Recipe 9.3.5 [Viewing Underlined Text], page 226.

3 A method for printing files with this markup is described in Recipe 25.3.5 [Preparing Text for Printing], page 522.

4 Another variation, though much less popular, is to use forward-slash characters, like " /this/ ".

The following recipes are for placing, converting, or removing these different types of underlines in text.

### 13.9.1 Placing Underlines in Text

There are different methods of placing underlines in text, depending on whether they are etext-style or overstrike-style underlines.

# METHOD #1

To place “_etext-style_” underlines in text, you just type an underscore character before and after the text to be underlined. (Another variation is to use the underscore for any space characters within the underlined text, “_just_like_this_”)

# METHOD #2

To place an overstrike-style underline in some text, you need to insert a literal backspace character (“Control-H”) immediately after a character you want to underline, and follow that with an underscore character (_).

⇒ Here are two ways to use this.

- To write the word “END” with overstrike-style underlines in an Emacs buffer, type (all on one line):
  E⌃Q ⌃H _ ⌃Q
  ⌃H _ D ⌃Q ⌃H _

- To write the word “stress” with overstrike-style underlines when you are in input mode in Vi, type (all on one line):
  E⌃V ⌃H _ ⌃V
  ⌃H _ D ⌃V ⌃H _

NOTES: For more information on inserting control characters in Emacs and Vi, see Recipe 10.1.4 [Inserting Special Characters in Emacs], page 239 and Recipe 10.2.4 [Inserting Special Characters in Vi], page 251, respectively.

### 13.9.2 Converting Underlines in Text

Text markup languages use different methods for denoting italics; for example, in TeX or LaTeX files, italicized text is often denoted with brackets and the \it command, like “{\it this}.” (LaTeX files use the same format, but \emph is often used in place of \it.)

You can convert one form to the other by using the Emacs replace-regular-expression function and specifying the text to be replaced as a regexp (see Recipe 14.3 [Regular Expressions—Matching Text Patterns], page 335).

⇒ Here are some ways to use this.

- To replace plaintext-style italics with TeX \it commands, type:
  ⟨ALT⟩-(X) replace-regular-expression ⟨RET⟩
  _\(...\)_ ⟨RET⟩
  {\it \1} ⟨RET⟩

- To replace TeX-style italics with etext style underscores, type:
  ⟨ALT⟩-(X) replace-regular-expression ⟨RET⟩
  {\it \(...\)} ⟨RET⟩
  _\1_ ⟨RET⟩

Both of these examples use the special regexp symbol "\1," which matches the same text matched by the first "\( ... \)" construct in the previous regexp.

NOTES: For more information on regexp syntax in Emacs, consult its Info documentation (see Recipe 2.8.5 [Reading an Info Manual], page 48).

### 13.9.3 Removing Underlines from Text

There are two methods to remove underlines from text—the first removes the underlining, and the second removes the characters to be underlined, but not the underlines themselves.

# METHOD #1

To remove backspace underlining from text, use colcrt with the - option, as described in Method #3 of Recipe 9.3.5 [Viewing Underlined Text], page 226.

⇒ To output a file containing backspace underlining called zim.bibliography, writing to a new file called zimbib.txt with no underlines at all, type:

```
$ colcrt - zim.bibliography > zimbib.txt ⟨RET⟩
```

# METHOD #2

To remove any text that is marked with underlines and not remove the underlines themselves, send the text to col with the -b option. This removes all of the characters to be underlined, and the backspace character ("Control-H") that follows each one. The underline characters (_) are kept.
