
# 15.3 Searching More than Plain Text Files

The following recipes are for searching data other than in plain text files.

## 15.3.1 Matching Lines in Compressed Files
Matching lines in compressed files.

## 15.3.2 Matching Lines in Web Pages
Matching lines in Web pages.

### 15.3.1 Matching Lines in Compressed Files

Use zgrep to search through text in files that are compressed. These files usually have a `.gz` file name extension, and can't be searched or otherwise read by other tools without uncompressing the file first (for more about compressed files, see section Compressed Files).

The zgrep tool works just like grep, except it searches through the text of compressed files. It outputs matches to the given pattern as if you'd searched through normal, uncompressed files. It leaves the files compressed when it exits.

are exactly four characters long ^....$or^.{4}$
are exactly seventy characters long ^.{70}$
begin with an asterisk character ^\*
begin with `tow' and end with `ing' ^tow.*ing$
contain a number [0-9]
do not contain a number ^[^0-9]*$
contain a year from 1991 through 1995 199[1-5]
contain a year from 1957 through 1969 \(195[7-9]\)\|\(196[0-9]\)
contain either `.txt' or `.text' \.te?xt
contain `cat' then `gory' in the same word cat\..+gory
contain `cat' then `gory' in the same line cat\..+\?gory
contain a `q' not followed by a `u' q[^u]
contain any ftp, gopher, or `http' URLs \(ftp\|gopher\|http\)://.*\.*
contain `N', `T', and `K', with zero or more characters between each N.*T.*K

### 15.3.2 Matching Lines in Web Pages

You can grep a Web page or other URL by giving the URL to lynx with the `-dump` option, and piping the output to grep.

- To search the contents of the URL http://example.com/ for lines containing the text `gonzo` or `hunter`, type:

```
$ lynx -dump http://example.com/ | grep 'gonzo\|hunter' RET
```

# 15.4 Outputting the Context of a Search

It is sometimes useful to see a matched line in its context in the file—that is, to see some of the lines that surround it.

Use the `-C` option with grep to output results in context—it outputs matched lines with two lines of "context" both before and after each match. To specify the number of context lines output both before and after matched lines, use that number as an option instead of `-C`.

- To search `/usr/dict/words` for lines matching `tsch` and output two lines of context before and after each line of output, type:

```
$ grep -C tsch /usr/dict/words RET
```

- To search `/usr/dict/words` for lines matching `tsch` and output six lines of context before and after each line of output, type:

```
$ grep -6 tsch /usr/dict/words RET
```

To output matches and the lines before them, use `-B`; to output matches and the lines after them, use

- To search through the compressed file `README.gz` for the text `Linux`, type:

```
$ zgrep Linux README.gz RET
```

`-A`. Give a numeric option with either of these options to specify that number of context lines.

- To search `/usr/dict/words` for lines matching `tsch` and output two lines of context before each line of output, type:

```
$ grep -B tsch /usr/dict/words RET
```

- To search `/usr/dict/words` for lines matching `tsch` and output six lines of context after each line of output, type:

```
$ grep -A6 tsch /usr/dict/words RET
```

- To search `/usr/dict/words` for lines matching `tsch` and output ten lines of context before and three lines of context after each line of output, type:

```
$ grep -B10 -A3 tsch /usr/dict/words RET
```

# 15.5 Searching and Replacing Text

A quick way to search and replace some text in a file is to use the following one-line perl command:

```
$ perl -pi -e "s/oldstring/newstring/g;" filespec RET
```

In this example, oldstring is the string to search, newstring is the string to replace it with, and filespec is the name of the file or files to work on. You can use this for more than one file.

- To replace the string `helpless` with the string `helpful` in all files in the current directory, type:

```
$ perl -pi -e "s/helpless/helpful/g;" * RET
```

You can also search and replace text in an Emacs buffer; to do this, use the replace-regexp function and give both the expression to search for and the expression to replace it with.

- To replace the text `helpless` with the text `helpful` in the current buffer, type:
