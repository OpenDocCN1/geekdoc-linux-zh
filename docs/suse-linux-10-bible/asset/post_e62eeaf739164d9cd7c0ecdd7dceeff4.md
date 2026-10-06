
# 278 Part III ♦ Using the Command Line in SUSE Linux

U.S. Social Security numbers look something like this: 012-34-5678. (So again naively because there are rules about which numbers in this format are valid ones) a command like this could be used to match them:

```bash
# grep -E '[0-9]{3}- [0-9]{2}- [0-9]{4}' file
```

It is beyond the scope of this book to explore regular expression syntax in detail. Indeed, entire books have been written on the subject. But it should be clear that grep (particularly in combination with the other tools mentioned in this chapter) can be a very powerful tool.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_322_0.png)

There is some but somewhat documentation for regular expressions with grep in the regular expressions section of the grep page; type info grep. There are a number of tutorials on the web one including IBM's Developer Works sites at www-106.ibm.com/developerworks/linux/edu-1-dw-linuxregexp-i.html.

# zgrep

The zgrep command is to grep zcat is to cat: in other words, it does the job of grep on zipped files. Here is a genuinely useful example:

```bash
user@bible:media/cdrom/ - zgrep kernel-source INDEX.gz
./CD1/suse/i586/kernel-source-2.6.4-52.i586.rpm
./CD2/user/src/kernel-source-2.6.4-52.src.rpm
```

The full listing of every SUSE version is contained in a zipped file INDEX.gz on the distribution media. We have used zgrep to find a particular package.

# grepmail

The grepmail command is a grep-like tool that looks for a string or regular expression in a Unix-style mailbox and outputs the entire mail or mails that contain the pattern. If you redirect the output to a new file, that file will be a mailbox consisting of exactly the mails you were looking for, which you can open in your mail client.

Here is a simple example:

```bash
user@home/user/mail > grepmail Lindsay inbox
From person@somedomain.com Tue Aug 10 09:14:34 2004
Return-path: <person@somedomomain.com>
Envelop-to: person@somedomomain.com
Delivery-date: Tue, 10 Aug 2004 09:14:34 +0100
Received: from person by somedomomain.com with local (Exim 3.35 #1 (Debian))
id 1BuRuME-007X-00
```

# Chapter 10 ✦ Text Manipulation 279

```bash
for <person@somomain.com>; Tue, 10 Aug 2004 09:14:34 +0100
Date: 10 Aug 2004 09:14:34 +0100
To: person@somomain.com
Subject: Mail with special word included
Message-ID: <200408001434.GAJ0335@somomain.com>
Mime-Version: 1.0
Content-Type: text/plain; charset=us-ascii
Content-Disposition: inline
User-Agent: Mutt/1.3.28i
From: Roger Whittaker <person@somomain.com>
Status: RD
Content-Length: 106
Lines: 5
```

This mail includes the word "Luxbierwanderung".
It also contains some other words.

- Roger Whittaker

You see the mail (or mails) with full headers from the inbox file that matches the expression given. The grepmail command has options that also enable you to add date and size specifications to the search.

# sgrep

The grep command is structured grep and enables you to extract sections from structured files (rather as grep does, but allowing for much more general types of files). It allows to extract particular sections from, for example, XML or HTML files (based on the content and the markup surrounding them) or from source files, mailboxes, or any file with a known and defined structure. The reason for mentioning it is to alert you to its existence; it may be by far the quickest way to extract information from files with a known structure and save you from having to write complex scripts.

Here is a simple example:

```bash
user@bible:- ~ cat index.html
<html>
<head>
<title>Web Page Title</title>
</head>
<body>
...

user@bible:- ~ sgrep "<title>\"</title>" index.html
Web Page Title
```

# 280 Part III ♦ Using the Command Line in SUSE Linux

Here you are searching for text enclosed by the opening and closing HTML title tags, and the command outputs the relevant string.

# split

The `split` command does what it says: it splits a file into parts. By default it splits the file into pieces, each of which has 1,000 lines with names xaa, xab, xac, and so on. The `split` command can also be used to split up a binary file into equal sized pieces; this can be useful in cases where the only way to get off a file is to copy to a floppy disk, and the file is too big. To reassemble the file, use `cat`. Consider the following examples:

```bash
user@bible:- > split -l 100000 ARCHIVES
```

This first example splits the file ARCHIVES into pieces with 100,000 lines each, with names xaa, xab, xac, and so on.

```bash
user@bible:- > split -b 1024k kernel-source-2.6.4-52.1586.rpm
```

This second example splits the file `kernel-source-2.6.4-52.1586.rpm` into pieces 1MB with names xaa, xab, xac, and so on. Assuming these files have all been copied into a directory elsewhere, to reassemble the original file, you simply use the following command:

```bash
cat x* > kernel-source-2.6.4-52.1586.rpm
```

Because the shell interprets the `*` as a list of all matching files in alphabetical order, the files will be concatenated in the right order and the result will be identical to the original.

# csplit

The `csplit` command enables you to split the file wherever a pattern is found in a line:

```bash
user@bible:- > cat birds
albatross
blackbird
chaffinch
duck
eagle
fieldfare
```

```bash
user@bible:- > csplit birds /finch/
20
31
```

```bash
user@bible:- > ls -1
```

# Chapter 10 ♦ Text Manipulation 281

```bash
-rw-r--r-- 1 user users 51 2004-06-10 10:47 birds
-rw-r--r-- 1 user users 20 2004-06-10 12:20 xx00
-rw-r--r-- 1 user users 31 2004-06-10 12:20 xx01
```

```bash
users@bible:- > cat xx00
albatross
blackbird
```

```bash
user@bible:- > cat xx00
user@bible:- > cat xx01
chaffinch
duck
```

# 326

# Working with Fields from Text

The commands discussed in this section enable you to work with text files in which each line is regarded as made up of fields.

# cut

If you have a file that consists of lines split into fields by white space or a delimiter character, cut can get a particular field or fields from every line. For example, in /etc/passwd the file is delimited by the colon (:). The cut option -f tells it which field you selecting, and the -d option tells it what delimiter.

```
user:x:1001:100:Guest User:/bin/bash
```

To get just the real name (the fifth) and the shell (the seventh) fields from the file, you could do this:

```bash
user@bible:~ cut -d -f5,7 /etc/passwd
```

This would produce many lines of output like this:

```
Guest User:/bin/bash
```

You can also select particular characters from each line, using the -c option:

```bash
user@bible:~ cut -c2-4 file
first
second
third
fourth
irs
eco
hir
our
```

# 327

# paste

The paste command takes corresponding lines from a set of files and puts them together into lines in its output. These examples should be enough to give you a general idea:

```bash
user@bibfile:~ ~ cat file1
1
2
3
```

```bash
user@bibfile:~ ~ cat file2
A
B
C
```

```bash
user@bibfile:~ ~ cat file3
X
Y
Z
```

```bash
paste file1 file2 file3
1 A X
2 B Y
3 C Z
```

In this example, you have put together corresponding lines from the three files in the order given, with white space between them.

```bash
paste -d: file1 file2 file3
1:A:X
2:B:Y
3:C:Z
```

In this example, by specifying -d: you have forced the delimiter in the output to be colon, rather than the default spaces.

# join

The join command takes two files with lines split into fields, and where a particular field is identical, it takes the other fields from both files and combines them. What follows is a simple example. (There are, course., options to control which field is regarded as the key.)

```bash
user@bibfile:~ ~ cat file1
001 beef
002 beer
003 pies
```
