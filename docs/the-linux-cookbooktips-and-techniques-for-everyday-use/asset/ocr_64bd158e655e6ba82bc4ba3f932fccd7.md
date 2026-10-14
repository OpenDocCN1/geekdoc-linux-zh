# 11.6.2 Appending Text to a File

To add text to a text file without opening the file in a text editor, use cat with the append operator, `>>`. (Using `>` instead would overwrite the file.)

+   - To add a line of text to the bottom of file `novels`, type:

```
$ cat 62;62; novels RET
The Last Tycoon RET
C-d
```

In this example, no files were specified to cat for input, so cat used the standard input; then, one line of text was typed, and this text was appended to file `novels`, the file used in the example of the previous recipe. So now this file would contain the following:

```
This Side of Paradise
The Beautiful and Damned
The Great Gatsby
Tender Is the Night
The Last Tycoon
```

# 11.6.3 Inserting Text at the Beginning of a File

@sf(WWW): http://dsl.org/comp/tinutils/

Inserting text at the beginning of a text file without calling up a text editor is a bit trickier than appending text to a file's end—but it is possible.

To insert one or more lines of text at the beginning of a file, use ins. Give the name of the file in which to insert text as an argument; ins will read lines of text from the standard input and insert them at the beginning of the file. (It works by opening the file in ed, a simple line editor.)

Give the EOF—that is, type C-d on a line by itself—to signify the end of the lines of text to insert.

+   - To insert several lines of text at the beginning of the file `novels`, type:

```
$ ins novels RET
The Novels of F. Scott Fitzgerald RET
---------------------------------------- RET
C-d
$
```