To find a file by its name, you will need to know a portion of the name.
The more of the name you give, the quicker the search will be because that will narrow down the results. You can use wildcards to specify unknown characters. This same functionality can be seen in just any other operating system, especially in Microsoft Windows. You can specify more than one file with a path using wildcards. A wildcard is a character that matches many characters. The * wildcard matches any number of characters. A wildcard will be explained more thoroughly and used in other (and more detailed) examples throughout the book.

If you do not know the name or part of the name, you will need to know something about the file. Things that can be used as searchable criteria include creation date and the size of the file. The find command can then be used to build up matches to the query you construct and execute to find the data you need. In the next exercise we will learn how to use the find command.

To search for a file by name:

+   - Before you search for a file, you have to have an idea of what you want to search for; therefore, specify the filename or some of its searchable criteria. Remember, you can include wildcards in the search for the filename.

+   - Next, select the directory you want to search. The starting directory will be /.

+   - This command would appear as find <starting directory> name <filename>.print, or if you wanted to find a specific file in the root directory, it would appear as follows:

```
>find / -name *.rm -print
/var/lib/Yast2/you/mnt/i386/update/9.2/deltas/kernel-source-2.6.8-24_24.i386.rpm
```

> Find Files...Now What? If you ask Unix to search for a file and do not tell it to print the results, Unix may find your file and tell you nothing about it. In most distributions of Unix, you will have to specify -print.