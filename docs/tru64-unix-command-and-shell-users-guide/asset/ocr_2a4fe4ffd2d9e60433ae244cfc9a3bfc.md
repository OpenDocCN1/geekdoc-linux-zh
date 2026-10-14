```
10d11
< howard
$
```

Here we find that Brent and Carol attended the meeting on January 22, and Howard did not. We know this because the line number and text output indicate that brent and carol are additions to file jan22mtg and that howard is a deletion.

In cases where there are no differences between files, the system will return merely your prompt. For more information, see the diff(1) reference page.

# 3.8 Sorting File Contents (sort)

You can sort the contents of text files with the sort command. You can use this command to sort a single file or multiple files.

The format of the sort command is:

```
sort filename
```

The filename entry can be the name of the file, the relative pathname of the file, the full pathname of the file, or a list of file names separated by spaces. You may also use pattern-matching characters to specify files. See Chapter 2 for information about pattern matching.

A good example of what the sort command can do for you is to sort a list of names and put them in collated order as defined by your current locale. For example, assume that you have lists of names that are contained in three files, list1, list2, and list3:

| list1 | list2 | list3 |
|---|---|---|
| Zenith, Andre | Rocca, Carol | Hamilton, Abe |
| Dikson, Barry | Shepard, Louis | Anastio, William |
| D'Ambrose, Jeanette | Hillary, Mimi | Saluccio, William |
| Julio, Annette | Chung, Jean | Hsaio, Peter |

To sort the names in all three files, enter:

```
$ sort list*
Anastio, William
Chung, Jean
D'Ambrose, Jeanette
Dickson, Barry
Hamilton, Abe
Hillary, Mimi
Hsaio, Peter
Julio, Annette
Rocca, Carol
```