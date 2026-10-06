
The grep utility can search for a pattern that is a simple string of characters. The following command line searches testa for and displays each line containing the string bb:

```
$ grep bb testa
aaabb
bbbcc
```

The -v option reverses the sense of the test. The following example displays all the lines without bb:

```
$ grep -v bb testa
ff-ff
ccccd
dddaa
```

The -n option displays the line number of each displayed line:

```
$ grep -n bb testa
1:aabb
2:bbbbcc
```

The grep utility can search through more than one file. Here grep searches through each file in the working directory. (The ambiguous file reference * matches all filenames.) The name of the file containing the string precedes each line of output:

```
$ grep bb *
testa:aabb
testb:bbbbcc
testb:bbbbb
```

When the search for the string bb is done with the -w option, grep produces no output because none of the files contains the string bb as a separate word:

```
$ grep -w bb *
$
```

The search that grep performs case sensitive. Because the previous examples specified lowercase bb, grep did not find the uppercase string, BBBBB, in testa. The -i option causes both uppercase and lowercase letters to match each letter of letter in the pattern:

```
$ grep -i bb *
testa:aabb
testb:bbbbcc
testb:bbbbb
testc:BBBBB
$ grep -i BB *
testa:aabb
testb:bbbbcc
testb:bbbbb
testc:BBBBB
```

The -c option displays the number of lines in each file that contain a match:

```
$ -c bb *
testa:2
testb:1
testc:0
```

The following command line displays from the file text2 lines that contain a string of characters starting with st, followed by zero or more characters (.*) represents zero or more characters in a regular expression—see Appendix A) and ending in:

```
$ grep 'st.*ing' text2
```

The regular expression, which matches the beginning of a line, can be used alone to match every line in a file. Together with the -n option, ^ can be used to display the lines in a file, preceded by their line numbers.

```
$ grep -n '^' testa
1:aaabb
2:bbcc
3:ff-ff
4:ccddd
5:dddaa
```

The next command line counts the number of times #include statements appear in C files in the working directory. The -h option causes grep to suppress filenames from its output. The input to sort is all lines with *.c that match #include. The output from sort is an ordered list of lines that contain many duplicates. When uniq with the -c option processes this, it outputs repeated lines only once, along with a count of the number of repetitions in its input:

```
$ grep -h '^include' *.c | sort | uniq -c
9 #include "buff.h"
2 #include "poly.h"
1 #include "screen.h"
6 #include "window.h"
2 #include "x2.h"
2 #include "x3.h"
2 #include <math.h>
3 #include <stdio.h>
```

The final command line calls the vi with a list of files in the working directory that contain the string Sampson. The $(...) command substitution structure (page 575) causes the shell to execute grep in place and supply vi with a list of file names you want to edit:

```
$ grep -1 'Sampson' *
```

The single quotation marks are not necessary in this example, but they are required if the string you are searching for contains special characters or spaces. It is generally a good habit to quote the pattern so that the shell does not interpret any special characters it may contain.

# gzip

## Compresses or decompresses files

gzip [options] / [file-list]

The gzip utility compresses files, reducing disk space requirements and the time needed to transmit files between computers. When gzip compresses a file, it adds the extension .gz to the filename: Compressing the file name creates the file fname.gz and deletes the original file. To restore fname, use the command gzip with the argument fname.gz. The .gz extension is optional.

## Arguments

The file-list is a list of one or more files that are to be compressed or decompressed. A directory appears in file-list with no --recursive option, gzip issues an error message and ignores the directory. With the --recursive option, gzip recursively compresses files within the directory and subdirectories to any level.

If file-list is empty or if the special option -o is present, gzip reads from standard input. The --force option permits standard input to come from the terminal and causes gzip to write to standard output.

The information in this section is also true of gunzip, a link to gzip.

## Options

- -decompress -d Decompresses a file with gzip. This option with gzip is equivalent to --uncompress
- -fast -best Gives you control over the speed of compression and the amount of compression. In the form -#, replace the # with a digit from 1 to 9: level 1 is the fastest compression and level 9. The default level is 6. The options -fast --best are synonyms for -1 and -9, respectively.
- -force -f Forces compression even if a file already exists, has multiple links.
- -recursive -r Recursively compresses files within the directory and subdirectories to any level.
- -stdout -c Writes the results of compression to standard output instead of overwriting.
- -verbose -v Displays the name of the file.

## Discussion

Almost all files become smaller when compressed. Rarely, files become larger, but only by a slight amount. The attributes of a file, such as owner, permissions, and modification times, are left intact.

If the compressed version of a file already exists, gzip asks for confirmation. If a file has multiple links, gzip terminates. The --force option overrides the default in both situations.

## Notes

In addition to the gzip format, gunzip recognizes several compressed-formats.

To see an example of a file that gets larger when compressed, you need to rename the file before compressing it again time.

## Examples

In the first example, gzip compresses two files. Next, gunzip decompresses one of the files. When a file is compressed and decompressed, its size changes, but its modification time remains the same:

```
$ ls -l
total 175
-rw-rw-r-- 1 alex group 33557 Jul 20 17:32 patch-2.0.7
-rw-rw-r-- 1 alex group 143258 Jul 20 17:32 patch-2.0.8
$ gzip ☆
```

```
$ ls -l
total 51
-rw-rw-r-- 1 alex group 9693 Jul 20 17:32 patch-2.0.7.gz
-rw-rw-r-- 1 alex group 40426 Jul 20 17:32 patch-2.0.8.gz
$ gzip patch-2.0.7.gz
$ ls -l
total 75
-rw-rw-r-- 1 alex group 33557 Jul 20 17:32 patch-2.0.7
-rw-rw-r-- 1 alex group 40426 Jul 20 17:32 patch-2.0.8.gz
```

In the next example the files in Jenny's home directory are archived using the cpio utility. The archive is compressed with gzip before it is written to tape:

```
$ find /home/jenny -depth -print | cpio -obm | gzip >/dev/ftape
```

For more information, refer to cpio on page 1124.
