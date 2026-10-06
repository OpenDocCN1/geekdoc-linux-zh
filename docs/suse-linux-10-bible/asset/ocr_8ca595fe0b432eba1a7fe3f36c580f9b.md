# Chapter 14 ◆ Working with the System 399

Variables can equally represent strings:

```
#! /bin/bash
a=ABCDE
echo $a
echo ${a}FGHIJ
```

```
ABCDE
ABCDEFGHIGHJ
```

Here, to get the desired result, you had to write ${a}FGHIJ rather than $aFGHIJ, which would have represented a new and as undefined variable (named aFGHIJ). This ensures that bash interprets the last line as a to echo the variable, which we defined as a, followed immediately by the string FGHIJ.

Suppose you want to produce word count for all the files with the file extension .txt in the current directory.

```
#! /bin/bash
for i in *.txt
do
wc -l $i
done
```

This produces output as shown in the following lines, indicating that you can loop over a set of files produced by globbing—the use of a notation such as *.txt.

```
3 1.txt
8 2.txt
17 3.txt
```

Clearly you could take this idea further to select, for example, certain lines from each set of files and append them to a file:

```
#! /bin/bash
for i in *.html
do
grep -i \<title> $i >>titles.list
done
```

This creates a file containing all lines of the form:

```
<title>Page Title</title>
```

from any of the HTML files in the current directory. Or you could do anything else that can be done with one or more commands acting on each file and direct the output to another.