
chown false mknod sed ypdomainname
cp fgrep more setserial zcat
cpio gawk mount sh
csh grep mt sleep
date gunzip mv sort

**NEW TERM** Regular expressions are a language of special string specification patterns. The ls command supports using wildcards and regular expressions, which means you can use options similar to and much more complex than the examples you saw with the find and locate commands. For example, if you only want to search for text files in the current directory, you can use the following:

```
# ls *.txt
```

Finally, if you want to see all the files on your system, you can use the ls -R option, which recursively descends directories to show you their contents. Although you can use this approach to search for files and build a catalog of the files on your system, be warned that it might take several minutes to list your files. The listing might also include files you don't want listed or files on other operating system file systems, such as DOS or Windows, especially if you use the following:

```
# ls -R /
```

A better approach might be to use the -d option with -R to list only a certain number of directory levels. For example, the following command searches three directory levels along the root (/) directory:

```
# ls -Rd /*/*/*
```

However, there's a much better utility for getting a picture of the directory structure of your system—tree—which is discussed in the following section.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_103_0.png)

> Do you like how ls -AF shows your directories? Do you prefer ls to use colors all the time? If you want the ls command to always show this sort of detail, see Hour 6.

## Listing Directories with the dir and vdir Commands

If you just can't get the hang of using ls to list your directories, you can use the dir or vdir commands. These commands have only about 45 command-line options compared to ls, but they're just as capable. They work like ls but with certain defaults.

The dir command works like the default ls command, listing the files in sorted columns as in the following example:

```
# dir
01_hyph.dat    49_thes.dat    bin            help           store
01_spell.dat   Desktop        config         install.ini    template
01_thes.dat    LICENSE        database       instdb.ins     wordbook
44_hyph.dat    README         download       kino           xp3
44_spell.dat   addin          explorer       l_soffice.xpm
44_thes.dat    autotext       filter         lib
49_hyph.dat    backup         fonts          s_soffice.xpm
49_spell.dat   basic          gallery        sofficecrc
```

The vdir command works like the ls -l option and presents a long format listing by default as follows:

```
# vdir
total 3659
-rw-rw-rw- 1 bball users 65605 Oct 27 10:00 01_hyph.dat
-rw-rw-rw- 1 bball users 313015 Oct 27 10:00 01_spell.dat
-rw-rw-rw- 1 bball users 375808 Oct 27 10:00 01_thes.dat
-rw-r--r-- 1 bball users 65605 Oct 27 10:00 44_hyph.dat
-rw-r--r-- 1 bball users 313015 Oct 27 10:00 44_spell.dat
-rw-r--r-- 1 bball users 380928 Oct 27 10:00 44_thes.dat
-rw-rw-rw- 1 bball users 51765 Oct 27 10:00 49_hyph.dat
-rw-rw-rw- 1 bball users 602497 Oct 27 10:00 49_spell.dat
-rw-rw-rw- 1 bball users 1191936 Oct 27 10:00 49_thes.dat
drwxr-xr-x 2 bball users 1024 Dec 2 11:21 Desktop
-rw-r--r-- 1 bball users 11631 Oct 27 10:00 LICENSE
-rw-r--r-- 1 bball users 8435 Oct 27 10:00 README
drwxr-xr-x 3 bball users 1024 Dec 2 11:21 addin
drwxr-xr-x 2 bball users 1024 Dec 2 11:21 autotext
drwxr-xr-x 2 bball users 1024 Dec 30 15:41 backup
drwxr-xr-x 2 bball users 1024 Dec 17 11:43 basic
drwxr-xr-x 2 bball users 2048 Dec 2 11:22 bin
drwxr-xr-x 11 bball users 3072 Jan 4 09:52 config
drwxr-xr-x 2 bball users 1024 Dec 2 11:30 database
drwxr-xr-x 2 bball users 1024 Dec 2 11:20 download
drwxr-xr-x 2 bball users 1024 Dec 2 11:20 explorer
drwxr-xr-x 2 bball users 1024 Dec 2 11:22 filter
drwxr-xr-x 4 bball users 1024 Dec 2 11:20 fonts
drwxr-xr-x 14 bball users 2048 Dec 2 11:22 gallery
drwxr-xr-x 4 bball users 1024 Dec 2 11:21 help
-rw-r--r-- 1 bball users 15569 Dec 2 11:22 install.ini
-rw-r--r-- 1 bball users 274209 Dec 17 11:20 instdb.ins
drwxr-xr-x 2 bball users 1024 Dec 2 11:21 kino
-rw-r--r-- 1 bball users 5199 Oct 27 10:00 l_soffice.xpm
drwxr-xr-x 2 bball users 3072 Dec 2 11:21 lib
-rw-r--r-- 1 bball users 812 Oct 27 10:00 s_soffice.xpm
-rw-r--r-- 1 bball users 8406 Jan 4 09:52 sofficecrc
drwxr-xr-x 3 bball users 1024 Dec 2 11:38 store
drwxr-xr-x 13 bball users 1024 Dec 17 11:43 _template
drwxr-xr-x 2 bball users 1024 Dec 2 12:08 wordbook
drwxr-xr-x 5 bball users 1024 Dec 2 11:20 xp3
```

Although you don't find separate manual pages for dir or vdir (they're mentioned in the ls man page), you can get help with each command by using the --help option.

## Listing and Combining Files with the cat Command

The cat (concatenate file) command is used to send the contents of files to your screen. You can also use this command to send files' contents into other files, too, using a process called output redirection. This section shows you some basic uses for this command. See Hour 6 for more about standard input, standard output, and redirection. Although cat can be useful for reading short files, it is usually used either to combine, create, overwrite, or append files. To use cat to look at a short file, you can enter the following:

```
# cat test.txt
This text file was created by the cat command.
Cat could be the world's simplest text editor.
If you read this book, you'll learn how to use cat.
This is the last line of text in this file.
```

The cat command also has a number of options. If you'd like to see your file with line numbers, perhaps to note a specific phrase, you can use the -n option:

```
# cat -n test.txt
1 This text file was created by the cat command.
2 Cat could be the world's simplest text editor.
3 If you read this book, you'll learn how to use cat.
4 This is the last line of text in this file.
```

You can also use cat to look at several files at once because cat accepts wildcards:

```
# cat -n test*
1 This text file was created by the cat command.
2 Cat could be the world's simplest text editor.
3 If you read this book, you'll learn how to use cat.
4 This is the last line of text in this file.
5 This is the first line of test2.txt.
6 This file was also created by cat.
7 This is the last line of test2.txt.
```

As you can see, cat also includes a second file in its output and numbers each line of the output, not each file. Note that you can also see both files with the following:

```
# cat test.txt test2.txt
```

The output is exactly the same as if you used a wildcard.

But looking at several files is only one way to use cat. You can also use the cat command with the redirection operator (>) to combine files. For example, if you want to combine test.txt and test2.txt into a third file called test3.txt, you can use the following:

```
# cat test* > test3.txt
```

You can check the result as follows:

```
# ls -l test*
-rw-r--r-- 1 bball users 190 Jan  4 16:06 test.txt
-rw-r--r-- 1 bball users 108 Jan  4 16:07 test2.txt
-rw-r--r-- 1 bball users 298 Jan  4 16:07 test3.txt
```

But what if you want to combine test.txt and test2.txt without creating a larger, third file? In this case, you first decide whether you want the contents of test.txt to go into test2.txt or the contents of test2.txt to go into test.txt. Then, using cat with the >> redirection operator, you type the following:

```
# cat test.txt >> test2.txt
```

This appends the contents of test.txt to the end of the test2.txt. To check the results, use cat again:

```
# cat test2.txt
This is the first line of test2.txt.
This file was also created by cat.
This is the last line of test2.txt.
This text file was created by the cat command.
Cat could be the world's simplest text editor.
If you read this book, you'll learn how to use cat.
This is the last line of text in this file.
```

Note that you can instead enter the command as follows:

```
# cat -n test.txt >> test2.txt
```

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_106_0.png)
