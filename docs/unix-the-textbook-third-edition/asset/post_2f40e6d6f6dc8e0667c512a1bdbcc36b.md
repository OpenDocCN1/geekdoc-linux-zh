
Note that the lines in the students file are sorted in ascending order by all characters, going from left to right (the whole line is used as the sort key). The following command sorts the file by using the whole line, starting with the last name—the second field (field number 1)—as the sort key.

```
% sort +1 students
Jamie Davidson    j.davidson@uet.edu    515.001.1212
John Johnsen      j.johnsen@psu.net     301.999.8888
John Johnsen      john.johnsen@tp.com   503.555.1111
David Kendall     d_kendall@msnbc.org   229.111.2013
Kelly Kimberly    kellyk@umich.gov      555.123.9999
Hassaan Sarwar    hsarwar@k12.st.or     503.444.2132
Ibraheem Sarwar   ibraheem@abc.sci.com  222.123.4567
Nabeel Sarwar     n.sarwar@xyz.net      434.555.1212
Maham Sarwar      smsarwar@k12.st.or    713.888.0000
%
```

The following command sorts the file in reverse order by using the phone number as the sort key and ignoring leading blanks (spaces and tabs). The +3 option specifies the phone number to be the sort key (as phone number is the last field), the -r option informs sort to display the sorted output in reverse order, and the -b option asks the sort utility to ignore the leading white spaces between fields.

```
% sort +3 -r -b students
Maham Sarwar      smsarwar@k12.st.or    713.888.0000
Kelly Kimberly    kellyk@umich.gov      555.123.9999
Jamie Davidson    j.davidson@uet.edu    515.001.1212
John Johnsen      john.johnsen@tp.com   503.555.1111
Hassaan Sarwar    hsarwar@k12.st.or     503.444.2132
Nabeel Sarwar     n.sarwar@xyz.net      434.555.1212
John Johnsen      j.johnsen@psu.net     301.999.8888
David Kendall     d_kendall@msnbc.org   229.111.2013
Ibraheem Sarwar   ibraheem@abc.sci.com  222.123.4567
%
```

The -b option is important if fields are separated by more than one space and the number of spaces differs from line to line, as is the case for the students file. The reason is that the space character is "smaller" (in terms of its ASCII value) than all letters and digits, and not skipping blanks will generate unexpected output. The sort keys can be combined, with one being the primary key and others being secondary keys, by specifying them in the order of preferences (the primary key occurring first). The following command sorts the students file with the last name as the primary key and the phone number as the secondary key.

## Commonly used options/features:

| Option | Description |
| --- | --- |
| `-exec CMD` | The file being searched meets the criteria if the command `CMD` returns 0 as its exit status (true value for commands that execute successfully); `CMD` must terminate with a quoted semicolon (`\;`). |
| `-inum N` | Search for files with inode number N. |
| `-links N` | Search for files with N links. |
| `-name pattern` | Search for files that are specified by the pattern. |
| `-newer file` | Search for files that were modified after file (i.e., are newer than file). |
| `-ok CMD` | Like `-exec` except that the user is prompted first. |
| `-perm octal` | Search for files if permission of the file is octal. |
| `-print` | Display the pathnames of the files found by using the rest of the criteria. |
| `-size ±N[c]` | Search for files of size N blocks; N followed by c can be used to measure size in characters; +N means size > N blocks, and -N means size < N blocks. |
| `-user name` | Search for files owned by the user name or ID name. |
| `\( expr \)` | True if expr is true; used for grouping criteria combined with OR or AND. |
| `! expr` | True if expr is false. |

More criteria are presented in Appendix A. You can use `[-a]` or a space to logically AND, and `-o` to logically OR two criteria. Note that at least one space is needed before and after an open parenthesis `\(` or a close parenthesis `\)`, and before and after `-o`. A complex expression can be enclosed in parentheses, `\(` and `\)`. We now discuss some illustrative examples.

The most common use of the find command is to search one or more directories for a file, as shown in the first example. Here, the command searches for the USA.gif and Pakistan.gif files in your home directory and displays the pathname of the directory that contains them. If the file(s) being searched for occurs in multiple directories, the pathnames of all the directories are displayed.

```
$ find ~ \( -name USA.gif -o -name Pakistan.gif \) -print
/home/sarwar/myweb/USA.html
/home/sarwar/myweb/Pakistan.html
$
```

The following command displays the absolute pathnames of all the files in your home directory that end in .c and .C

```
$ find ~ \( -name '*.c' -o -name '*.C' \) -print
...
$
```

The next command searches the /usr/include directory recursively for a file named socket.h and prints the absolute pathname of the file.
