# pr

The pr command takes a text file and splits it into pages of text separated by a number of newlines with a header on each page. Optional, it can add a form feed character between the pages for sending the output directly to a printer. For example, using the command with no options:

```
user@bible:- > README.txt
```

will output pages with a header on each looking like:

```
2004-08-10 12:26
INDEX
Page 1
```

# fold

The fold command formats a text file by breaking long lines. By default, the lines will be set to a maximum width of 80 characters. You can set the width of the lines you want in the output with the option -w, but if this is too small, the output may look bad.

A case where the fold command is useful is when you have saved a word document as plain text. In the text file, each paragraph will be a single line. A command such as fold -w 76 file.txt will break these lines sensibly.

# fmt

The fmt command takes some text (an article that you have written in a editor) and does some sensible reformatting to it. Provided that you have separated paragraphs by empty lines, fmt will combine broken lines and make all lines a sensible length. It can also ensure that words are separated by one space and sentences by two. In the example that follows, the -u option forces uniform spacing in other words, one space between words and two spaces between sentences.

```
user@bible:- > cat badfile
This is a file with some extra space and its line endings are in mess. We need to reformat it somehow.
```

```
user@bible:- > fmt -u badfile
This is a file with some extra space and its line endings in a mess. We need to reformat it somehow.
```