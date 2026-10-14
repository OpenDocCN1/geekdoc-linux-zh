# 13.5 Filtering Out Duplicate Lines of Text

There are two methods for filtering out duplicate lines of text.

# METHOD #1

The uniq tool outputs only the unique lines of its input—any lines occurring more than once are only output once. The input must be sorted; that is, duplicate lines must be neighboring (see Recipe 13.6 [Sorting Text], page 320).

⇒ To output the contents of the file options, with all duplicate lines filtered out, type:

```
$ uniq options [RET]
```

Use the -i option to ignore case when making comparisons.

⇒ To output the contents of the file options, with all duplicate lines filtered out, regardless of case, type:

```
$ uniq -i options [RET]
```

To output only the lines that have duplicates, use the -d option. To output only the lines that have duplicates, plus every instance of each duplicate line, use -D instead.

⇒ Here are two ways to use this.

+   - To output only the lines in the file options that have duplicates, but not the duplicates themselves, type:

```
$ uniq -d options [RET]
```

+   - To output all of the lines in the file options that have duplicates, and all the duplicates themselves, type:

```
$ uniq -D options [RET]
```

To output lines preceded by a count telling how many instances exist of that line, use the -c option.

⇒ To output all of the lines in the file options, each preceded by a count of the number of instances of that line, type:

```
$ uniq -c options [RET]
```

# METHOD #2

To filter out unique lines in some unsorted text, use sort with the -u option. This sorts the input lines alphabetically and runs uniq on them.