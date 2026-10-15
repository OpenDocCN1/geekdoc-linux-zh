# Contents of current directory

| Inode # | File |
|---|---|
| 1076 | . |
| 2083 | .. |
| 13059 | Chapter1 |
| 17488 | Chapter2 |
| 52473 | Chapter3 |
| 83476 | memo6.hard |

# Contents of ~/memos

| Inode # | File |
|---|---|
| 1076 | . |
| 2083 | .. |
| 83468 | memo01 |
| ... | ... |
| 83476 | memo6 |
| ... | ... |

![](bbox=[0.38, 0.35, 0.68, 0.62])

FIGURE 8.3 Pictorial representation of the hard link between ~/memos/memo6 and memo6.hard in the current directory.

write permissions to it. Note that the link counts for all the files in dir1 and dir2 are 2. The -f option is used to force creation of a hard link in case any of the files f1, f2, or f3 already exist in the ~/unixbook/examples/dir2 directory.

```
$ cd unixbook/examples
$ more dir1/f1
Hello, World!
This is a test file.
$ ls -l dir1
-rw------ 1 sarwar faculty 35 Jun 22 22:21 f1
-rw------ 1 sarwar faculty 68 May 16 21:03 f2
-rw------ 1 sarwar faculty 94 Jul 11 11:39 f3
$ ln -f ~/unixbook/examples/dir1/* ~/unixbook/examples/dir2
$ ls -l dir1
-rw------ 2 sarwar faculty 35 Jun 22 22:21 f1
-rw------ 2 sarwar faculty 68 May 16 21:03 f2
-rw------ 2 sarwar faculty 94 Jul 11 11:39 f3
$ ls -l dir2
-rw------ 2 sarwar faculty 35 Jun 22 22:21 f1
-rw------ 2 sarwar faculty 68 May 16 21:03 f2
-rw------ 2 sarwar faculty 94 Jul 11 11:39 f3
$ more dir2/f1
Hello, World!
This is a test file.
$
```