appends the contents of the memo1, memo2, and memo3 files at the end of the memos.record file.

```
$ cat temp
This is a simple file used to illustrate the working of append operation. The new data will be appended right below this line.
$ cat sample
These are the new data that will be appended at the end of the test file.
$ cat sample >> temp
$ cat temp
This is a simple file used to illustrate the working of append operation. The new data will be appended right below this line.
These are the new data that will be appended at the end of the test file.
$ cat memo1 memo2 memo3 >> memos.record
$
```

Without the optional file-list argument (see the command description), the command can be used to append keyboard input at the end of destination-file. The cat >> test.letter command below takes input from the keyboard and appends it to a file called test.letter. The command terminates when you press <Ctrl+D> on a new line.

```
$ cat test.letter
John Doe
12345 First Lane
Second City, State 98765
$ cat >> test.letter
September 1, 2014
Dear John:
This is to inform you ...
...
<Ctrl+D>
$ cat test.letter
John Doe
12345 First Lane
Second City, State 98765
September 1, 2014
Dear John:
This is to inform you ...
...
$
```

# 6.5 COMBINING FILES

The following command syntax can be used to combine multiple files into one file.