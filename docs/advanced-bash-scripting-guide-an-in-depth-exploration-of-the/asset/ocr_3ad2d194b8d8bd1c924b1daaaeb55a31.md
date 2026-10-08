# Advanced Bash-Scripting Guide

Using wc to count many .txt files are in current working directory:

```
$ ls *.txt | wc -1
# Will work as long as none of the "*.txt" files
#+ have a lifeless embedded in their name.

# Alternative ways of doing this are:
# find -maxdepth 1 -name '*.txt' -print 0 | grep -cz
# (shopt -s nullglob; set *.txt; echo $$)
```

# Thanks, S.
Using wc to total up the size of all the files whose names begin with letters in the range d-h

```
bash wc [d-]* | grep total | awk 'print $3'
71832
```

Using wc to count the instances of the word "Linux" in the main source file for this book.

```
bash grep Linux-book.sgml | wc -1
138
```

See also Example 16-39 and Example 20-8.

Certain commands include some of the functionality of wc:

```
... | grep foo wc -1
# This frequently used construct can be more concisely rendered.

... | grep -c foo
# Just use the "-c" (or "--count") option of grep.

# Thanks, S.
```

tr

character translation filter.

> Must use quoting/or brackets, as appropriate. Quotes prevent from reinterpreting the expression in tr commands. Brackets should be quoted to prevent expansion by the shell.
Either tr "A-Z" "*" <filename tr A-Z \* <filename changes all the uppercase letters to asterisk (writes to stdout). On some systems this may not work, tr A-Z '[\*]' will.

- -d option deletes a range of characters.

```
echo "abcdef" # abcdef
echo "abcdef" | tr -d b-d # aef

tr -d 0-9 <filename
# Deletes all digits from the file "filename".
tr --squeeze-repeats (or -s) option deletes all but the first instance of a string of consecutive characters. This option is useful for removing whitespace.
whitespace. This option is useful for removing whitespace.
```

Chapter 16. External Filters, Programs and Commands

250