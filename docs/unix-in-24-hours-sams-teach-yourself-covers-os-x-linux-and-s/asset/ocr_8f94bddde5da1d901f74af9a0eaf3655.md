# The awk Programming System

Whether it’s C, Pascal, BASIC, Java, or even Swift, every programming language has its forte, the area where it really shines. If it’s BASIC, it’s simple introductory programming. If it’s Java, it’s platform-independent software. Ruby, Python, C++, LISP, and all other programming languages have a specific type of programming for which they’re designed. awk is different, though, living somewhere in between simple shell scripts and these sophisticated languages. It doesn’t have many of the features and characteristics of a formal programming environment, but in its own way, awk is powerful, and it’s definitely ideal for lightweight, in-line data processing.

# Task 9.1: Learning to Use awk

The basic structure of every awk script is a pattern followed by a command. If you skip the pattern, the command applies to all lines in the data stream. If you skip the command section, all matching lines are printed (sent to the output data stream).

As a very simple example, the program NF == 3 (yep, that’s all you’d need for this program!) will print all lines of input that have exactly three fields (NF is a shortcut meaning number of fields in the input line). The program $1 > 3 { print $1 } will print the first field of all lines where that field has a numeric value greater than three.

Let’s take a closer look at awk.

+   1. I want to figure out the average size of all the email files on a new system I’ve been building. To accomplish this, I’ll start with ls to get the file sizes:

Click here to view code image

```
$ ls -l
total 8474
-rw-r--r-- 1 taylor taylor    3111 Dec 14 16:09 baby-responses
-rw-r--r-- 1 taylor taylor   19930 Dec 14 16:09 barbara
-rw-r--r-- 1 taylor taylor   298719 Dec 14 16:09 dunlap
-rw-r--r-- 1 taylor taylor    5758 Dec 14 16:09 evan
-rw-r--r-- 1 taylor taylor   14577 Dec 14 16:09 glee
-rw-r--r-- 1 taylor taylor    1610 Dec 14 16:09 hbrayman
-rw-r--r-- 1 taylor taylor   10788 Dec 14 16:09 jwickert
-rw-r--r-- 1 taylor taylor  2746614 Dec 14 16:09 mail.sent
-rw-r--r-- 1 taylor taylor   18106 Dec 14 16:09 mbeaudoin
-rw-r--r-- 1 taylor taylor    6753 Dec 14 16:09 pennyln
-rw-r--r-- 1 taylor taylor   128815 Dec 14 16:09 permission
-rw-r--r-- 1 taylor taylor  1011092 Dec 14 16:09 taylor
-rw-r--r-- 1 taylor taylor   17549 Dec 14 16:09 wellnitz
$
```

As you can see, the lines of output from ls are very consistent, and if you assume that “one or more spaces without any other characters between them” is the separator between fields and that the fifth field in the output is always the size of the file, you have a recipe for finding and processing the necessary data for a file size total within a directory.

+   2. Let’s use awk to extract the fifth field:

```
$ ls -l | awk '{print $5}'
```