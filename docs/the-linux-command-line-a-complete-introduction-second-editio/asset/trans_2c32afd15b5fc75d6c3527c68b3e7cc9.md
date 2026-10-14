

method of matching file and pathnames but on a much grander scale. Regular expressions are supported by many command line tools and by most programming languages to facilitate the solution of text manipulation problems. However, to further confuse things, not all regular expressions are the same; they vary slightly from tool to tool and from programming language to language. For our discussion, we will limit ourselves to regular expressions as described in the POSIX standard (which will cover most of the command line tools), as opposed to many programming languages (most notably Perl), which use slightly larger and richer sets of notations.

## grep

The main program we will use to work with regular expressions is our old pal grep. The name grep is actually derived from the phrase “global regular expression print,” so we can see that grep has something to do with regular expressions. In essence, grep searches text files for text matching a specified regular expression and outputs any line containing a match to standard output.

So far, we have used grep with fixed strings, like so:

```
[me@linuxbox ~]$ ls /usr/bin | grep zip
```

This will list all the files in the /usr/bin directory whose names contain the substring zip.

The grep program accepts options and arguments this way, where regex is a regular expression:

```
grep [options] regex [file...]
```

Table 19-1 describes the commonly used grep options.

Table 19-1: grep Options

| Option | Long option | Description |
|---|---|---|
| -i | --ignore-case | Ignore case. Do not distinguish between uppercase and lowercase characters. |
| -v | --invert-match | Invert match. Normally, grep prints lines that contain a match. This option causes grep to print every line that does not contain a match. |
| -c | --count | Print the number of matches (or non-matches if the -v option is also specified) instead of the lines themselves. |
| -l | --files-with-matches | Print the name of each file that contains a match instead of the lines themselves. |
| -L | --files-without-match | Like the -l option, but print only the names of files that do not contain matches. |
| -n | --line-number | Prefix each matching line with the number of the line within the file. |
| -h | --no-filename | For multifile searches, suppress the output of filenames. |

To more fully explore grep, let’s create some text files to search.

```
[me@linuxbox ~]$ ls /bin > dirlist-bin.txt
[me@linuxbox ~]$ ls /usr/bin > dirlist-usr-bin.txt
[me@linuxbox ~]$ ls /sbin > dirlist-sbin.txt
[me@linuxbox ~]$ ls /usr/sbin > dirlist-usr-sbin.txt
[me@linuxbox ~]$ ls dirlist*.txt
dirlist-bin.txt  dirlist-sbin.txt  dirlist-usr-sbin.txt
dirlist-usr-bin.txt
```

We can perform a simple search of our list of files like this:

```
[me@linuxbox ~]$ grep bzip dirlist*.txt
dirlist-bin.txt:bzip2
```

```
dirlist-bin.txt:bzip2recover
```

In this example, grep searches all the listed files for the string bzip and finds two matches, both in the file dirlist-bin.txt. If we were interested only in the list of files that contained matches rather than the matches themselves, we could specify the -l option.

```
[me@linuxbox ~]$ grep -l bzip dirlist*.txt
dirlist-bin.txt
```

Conversely, if we wanted to see only a list of the files that did not contain a match, we could do this:

```
[me@linuxbox ~]$ grep -L bzip dirlist*.txt
dirlist-sbin.txt
dirlist-usr-bin.txt
dirlist-usr-sbin.txt
```

## Metacharacters and Literals

While it might not seem apparent, our grep searches have been using regular expressions all along, albeit very simple ones. The regular expression bzip is taken to mean that a match will occur only if the line in the file contains at least four characters and that somewhere in the line the characters b, z, i, and p are found in that order, with no other characters in between. The characters in the string bzip are all literal characters, in that they match themselves. In addition to literals, regular expressions may also include metacharacters that are used to specify more complex matches. Regular expression metacharacters consist of the following:

```
^ $ . [ ] { } - ? * + ( ) | \
```

All other characters are considered literals, though the backslash character is used in a few cases to create metasequences, as well as allowing the metacharacters to be escaped and treated as literals instead of being interpreted as metacharacters.

